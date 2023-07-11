# Import Cloud Data

RedBrick AI can integrate with various cloud providers so that you don't have to upload data directly to RedBrick AI servers. To upload data from a cloud server, you need to do the following:&#x20;

RedBrick AI supports integration with a range of cloud providers, allowing you to make use of its suite of tools without having to dupload your data directly to our servers. You can upload data from a cloud server to RedBrick AI by following the steps below:

While the steps and configurations required for uploading data from cloud storage vary depending on your provider, the overall procedure remains the same:&#x20;

1. [Configure your cloud storage](import-cloud-data/creating-an-items-list.md) - AWS s3, Google Cloud Storage, Azure Blob Storage
2. Create and upload an Items List (see below) - your Items List communicates the location of your data in your cloud storage to RedBrick. After creating create an Items List, you can upload it via the [CLI](../python-sdk/cli-overview/) or the RedBrick web application.

## Items List

### Configuring Cloud Storage

The Items List defines your data’s storage location and structure. Each entry in your Items List will be created as a separate task, which can then be annotated as a single unit. You can find detailed explanations of each key in our [format reference](../python-sdk/reference/export-annotation-format.md#tasks-json).&#x20;

Please note that the example below contains fields relevant to image-only uploads.

RedBrick AI currently supports the following external storage methods:

{% hint style="info" %}
The `items` entry enumerates the file paths referencing your data in your cloud storage. Depending on the storage method, this file path may be relative to your bucket name or the root folder in your bucket.\
\
Please reference the relevant documentation to verify the format of the `items` path for each of RedBrick's supported storage methods:

* [AWS s3 items path](configuring-external-storage/configuring-aws-s3.md#items-path)
* [Azure Blob items path](import-cloud-data/configuring-azure-blob.md#items-path)
* [Google Cloud Storage items path](https://docs.redbrickai.com/importing-data/import-cloud-data/configuring-gcs#items-path)
* [Public Storage items path](https://docs.redbrickai.com/importing-data/import-cloud-data/creating-an-items-list#example-items-path)
{% endhint %}

* [AWS S3 Buckets](configuring-external-storage/configuring-aws-s3.md)
* [Google Cloud Storage](configuring-external-storage/configuring-gcs.md)
* [Azure Blob Storage](import-cloud-data/configuring-azure-blob.md)
* Public - this includes data stored on your computer, as well as data stored on any public server accessible via URL

{% tabs %}
{% tab title="3D DICOM Study" %}
This Items List will upload a single task containing two series.&#x20;

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
This Items List will upload two tasks, each containing a single series.

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

{% tabs %}
{% tab title="NIfTI Study" %}
This Items List will upload a single task containing two series. Please note that `items` must be a single string for NIfTI uploads.&#x20;

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
This Items List will upload two tasks, each containing a single series.

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

{% tabs %}
{% tab title="Image Study" %}
This Items List will upload a single task containing two images.&#x20;

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
This Items List will upload two tasks, each containing a single image.

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

{% tabs %}
{% tab title="Video Frames Study" %}
This Items List will upload a single task containing two videos with three frames each.

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
This Items List will upload two tasks, each containing one video with three frames.&#x20;

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
The frames must be ordered correctly in the `items` array.
{% endhint %}
{% endtab %}
{% endtabs %}

In some use cases, you can rely on RedBrick AI to split your Study into a list of Series. This can be especially useful if your Studies do not follow a strict naming convention.

If you find yourself in need of further clarification, we recommend consulting our in-depth configuration guides for the above third-party cloud storage solutions.

You can upload a single Series or multiple Series per task using the simplified Study-Level format.

Once you have configured your cloud storage, you can return to the RedBrick AI platform to proceed with creating and configuring your Storage Method.



### Creating & Configuring a Storage Method

After opening the Storage tab in the lefthand sidebar, click on **New Storage Method** to configure your new Storage Method for further use with RedBrick AI. After inputting the required credentials, click on **Create Storage** to integrate your cloud storage with RedBrick AI.

You can also make use of the **Verify** action to ensure that your file path has been correctly designated and integrated with RedBrick AI.



### Creating & Configuring an Items List

Your Items List is a JSON file that points the RedBrick AI platform to the data in your external storage and allows you to selectively import data points. It can be uploaded to RedBrick from the Project Dashboard or by using the [SDK](../python-sdk/sdk-overview/importing-data-and-annotations.md).

<figure><img src="../.gitbook/assets/items_list_popout.png" alt=""><figcaption><p>Clicking on Import Data will allow you to upload your Items List</p></figcaption></figure>

The format of your Items List depends on both the type of cloud storage you have integrated with RedBrick AI and the type of data you are uploading.

{% hint style="info" %}
This format is the same as the Legacy Items List format (pre-July 2022)
{% endhint %}

For solution-specific instructions regarding how to format your Items List with [AWS S3](configuring-external-storage/configuring-aws-s3.md#items-path), [GCS](configuring-external-storage/configuring-gcs.md#items-path), or [Azure Blob Storage](import-cloud-data/configuring-azure-blob.md#items-path), please refer to the corresponding configuration guide.

{% hint style="info" %}
Please note that there is no need to create an Items List when using [Direct Upload](direct-data-upload.md).
{% endhint %}

{% tabs %}
{% tab title="DICOM" %}
The Items List below will create one task containing one or more series. RedBrick AI will parse the DICOM files on the client side and automatically split this list of `.dcm` into one or more series (depending on the DICOM headers).&#x20;

This upload method can be helpful if you have a dump of `.dcm` files without a strict file naming convention.

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
Please note that any tasks uploaded using this format will only be split into a list of Series **after** being opened by a user in the labeling tool.
{% endhint %}

For a more detailed overview of how Items Lists work in RedBrick AI, as well as examples of how to format them with different data types, please consult our dedicated [guide](import-cloud-data/creating-an-items-list.md).



### Data Privacy

When using an external storage method with RedBrick AI, all of your data is transferred directly from your storage method to your browser.

<figure><img src="../.gitbook/assets/Group 476.png" alt=""><figcaption></figcaption></figure>

Your raw data will never be routed through RedBrick AI's servers, downloaded, or duplicated (unless specifically requested for certain features - please review our [Privacy Policy](https://redbrickai.com/policies/privacy.pdf)).&#x20;
