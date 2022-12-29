# Import Cloud Data

RedBrick AI can integrate with various cloud providers so that you don't have to upload data directly to RedBrick AI servers. To upload data from a cloud server, you need to do the following:&#x20;

1. [Configure your cloud storage](configuring-external-storage/) - AWS s3, Google Cloud Storage, Azure Blob Storage
2. [Create and upload an items list](import-cloud-data.md#create-and-upload-an-items-list) - Your items list tells RedBrick the location of your data in your cloud storage. Once you create an items list, you can upload it via the [CLI](broken-reference) or the UI.

{% hint style="success" %}
Please see [the following documentation](broken-reference) if you want to upload annotations with your data.
{% endhint %}

## Items list

The items list defines the storage location and structure of your data. Each entry in your Items list will be _**created as a separate task**_ on RedBrick AI (to be annotated as a single unit). Please see detailed explanations of each key in our [format reference](../python-sdk/reference/annotation-format.md#tasks-json) (note, the format reference has many extra fields, these are the ones relevant to image-only uploads).

```typescript
type Items = Task[];

interface Task {
  // A unique, user-defined ID
  // After import, you can search tasks using this field.
  name: string;

  // You can upload a single series, or an entire study (array of series)
  series: Series[];
}

interface Series {
  // Filepath/URL's of all the instances in a single series.
  items: string[] | string;
  name: string;
}
```

{% hint style="info" %}
The **`items`** entry enumerates file paths referencing your data in your cloud storage. Depending on the storage method, this file path may be relative to your bucket name or the root folder in your bucket. \
\
Please visit the relevant documentation to see the format of the `items` path for each of the storage methods:&#x20;

* [AWS s3 items path](configuring-external-storage/configuring-aws-s3.md#items-path)
* [Azure Blob items path](configuring-external-storage/configuring-azure-blob.md#items-path)
* [Google Cloud Storage items path](broken-reference)
* [Public Storage items path](broken-reference)
{% endhint %}

### Examples

#### 3D DICOM

{% tabs %}
{% tab title="3D DICOM Study" %}
This items list will upload a single task containing two series.&#x20;

```javascript
[
  {
    name: 'study001',
    series: [
      {
        items: [
          'study001/series001/001.dcm',
          'study001/series001/002.dcm',
          'study001/series001/003.dcm',
        ],
      },
      {
        items: [
          'study001/series002/001.dcm',
          'study001/series002/002.dcm',
          'study001/series002/003.dcm',
        ],
      },
    ],
  },
];
```
{% endtab %}

{% tab title="3D DICOM Series" %}
This items list will upload two tasks each containing a single series.

```javascript
[
  {
    name: 'series001',
    series: [
      {
        items: ['series001/001.dcm', 'series001/002.dcm', 'series001/003.dcm'],
      },
    ],
  },
  {
    name: 'series002',
    series: [
      {
        items: ['series002/001.dcm', 'series002/002.dcm', 'series002/003.dcm'],
      },
    ],
  },
];
```
{% endtab %}
{% endtabs %}

#### NIfTI

{% tabs %}
{% tab title="NIfTI Study" %}
This items list will upload a single task containing two series. `items` must be a single string for NIfTI uploads.&#x20;

```javascript
[
  {
    name: 'study001',
    series: [
      {
        items: 'series001.nii',
      },
      {
        items: 'series002.nii',
      },
    ],
  },
];
```
{% endtab %}

{% tab title="NIfTI Series" %}
This items list will upload two tasks each containing 1 series.

```javascript
[
  {
    name: 'series1',
    series: [
      {
        items: 'series001.nii',
      },
    ],
  },
  {
    name: 'series2',
    series: [
      {
        items: 'series002.nii',
      },
    ],
  },
];

```
{% endtab %}
{% endtabs %}

#### 2D Image

{% tabs %}
{% tab title="Image Study" %}
This items list will upload a single task containing two images.&#x20;

```javascript
[
  {
    name: 'patient1',
    series: [
      {
        items: 'scan1.dcm',
      },
      {
        items: 'scan2.dcm',
      },
    ],
  },
];
```
{% endtab %}

{% tab title="Image Series" %}
This items list will upload two tasks, each containing a single image.

```javascript
[
  {
    name: 'patient1',
    series: [
      {
        items: 'scan.dcm',
      },
    ],
  },
  {
    name: 'patient2',
    series: [
      {
        items: 'scan.dcm',
      },
    ],
  },
];
```
{% endtab %}
{% endtabs %}

#### Video Frames

{% tabs %}
{% tab title="Video Frames Study" %}
This items list will upload a single task containing two videos, each with three frames.&#x20;

```javascript
[
  {
    name: 'study001',
    series: [
      {
        items: [
          'study001/series001/001.png',
          'study001/series001/002.png',
          'study001/series001/003.png',
        ],
      },
      {
        items: [
          'study001/series002/001.png',
          'study001/series002/002.png',
          'study001/series002/003.png',
        ],
      },
    ],
  },
];
```

{% hint style="warning" %}
The frames must be in the correct order in the `items` array.
{% endhint %}
{% endtab %}

{% tab title="Video Frames Series" %}
This items list will upload two tasks, each containing 1 video with 3 frames.&#x20;

```javascript
[
  {
    name: 'video1',
    series: [
      {
        items: ['001.png', '002.png', '003.png'],
      },
    ],
  },
  {
    name: 'video2',
    series: [
      {
        items: ['001.png', '002.png', '003.png'],
      },
    ],
  },
];
```

{% hint style="info" %}
The frames must be in the correct order in the `items` array.
{% endhint %}
{% endtab %}
{% endtabs %}

## Automatically Split Study

In some use cases, you can rely on RedBrick AI for splitting your study into a list of Series. This can be especially useful if you do not follow a robust naming convention for your studies.

You can upload single or multiple series per task using the simplified Study level format.&#x20;

```javascript
type Items = Task[];

interface Task {
  // A unique, user-defined ID
  // After import, you can search tasks using this field.
  name: String;

  // You can upload a single series, or an entire study (array of .dcm files)
  // The items array will automatically be split into individual series. 
  items: String[]
}
```

{% hint style="info" %}
This format is the same as the Legacy items list format (pre-July 2022)
{% endhint %}

{% tabs %}
{% tab title="DICOM" %}
The items list below will create 1 task containing one or more series. RedBrick AI will parse the DICOM files on the client side and automatically split this list of `.dcm` into one or more series (depending on the DICOM headers).&#x20;

This upload method can be helpful if you have a dump of `.dcm` files without a robust file naming convention.

```javascript
[
  {
    name: 'study001',
    items: [
      'bbfa85feb36f.dcm',
      'd4a49634cd4c.dcm',
      'eed2e7462ba5.dcm',
      '45455dd0e45b.dcm',
    ],
  },
]
```
{% endtab %}

{% tab title="NIfTI" %}
The items list below will create 1 task containing exactly two series. RedBrick AI will assume each of the NIfTI files in the `items` array is an individual series.

```javascript
[
  {
    name: 'study001',
    items: [
      'bbfa85feb36f.nii.gz',
      'd4a49634cd4c.nii'
    ],
  },
]
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Please note that any tasks uploaded using this format will only be automatically split _**after**_ any user opens it in the labeling interface.&#x20;
{% endhint %}
