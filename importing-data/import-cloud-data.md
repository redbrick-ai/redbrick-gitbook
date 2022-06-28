# Import Cloud Data

RedBrick AI can integrate with various cloud providers so that you don't have to upload data directly to RedBrick AI servers. To upload data from a cloud server, you need to do the following:&#x20;

1. [Configure your cloud storage](configuring-external-storage/) - AWS s3, Google Cloud Storage, Azure Blob Storage
2. [Create and upload an items list](import-cloud-data.md#create-and-upload-an-items-list) - Your items list tells RedBrick where in your cloud storage data is. Once you create an items list, you can upload it via the [CLI](../python-sdk/cli-overview/importing-data/) or the UI

{% hint style="info" %}
If you want to upload annotations with your data, please see [the following documentation](../python-sdk/cli-overview/importing-annotations/nifti-segmentations.md)
{% endhint %}

## Items list

The items list has a single entry for a single task on RedBrick AI. Please see the definition below:

```typescript
type Items = Task[]
type Task = {
    items: String[],
    name: String
}
```

#### `items: String[]`

A list of file paths referencing your data in your cloud storage. Depending on the storage method, this file path may be relative to your bucket name, or the root folder in your bucket.&#x20;

{% hint style="info" %}
Please visit the relevant documentation to see the format of the `items` path for each of the storage methods:&#x20;

* [AWS s3 items path](configuring-external-storage/configuring-aws-s3.md#items-path)
* [Azure Blob items path](configuring-external-storage/configuring-azure-blob.md#items-path)
* [Google Cloud Storage items path](broken-reference)
* [Public Storage items path](broken-reference)
{% endhint %}

**`name: String`**

A user defined unique string to identify your task. We recommend making this a human readable string that makes it easy to search for your task e.g. `study01/series01`

## 3D DICOM Items List

For 3D DICOM datasets (`.dcm`) you can upload your data series-wise, where 1 task corresponds to a single series, or study-wise, where 1 task corresponds to multiple series.

### 3D DICOM Series

The following items list will create 2 tasks containing 1 series each.&#x20;

```json
[
  {
    "name": "series-001",
    "items": [
      "root-folder/series-1/instance1.dcm",
      "root-folder/series-1/instance2.dcm",
      "root-folder/series-1/instance3.dcm"
    ]
  },
  {
    "name": "series-2",
    "items": [
      "root-folder/series-2/instance1.dcm", 
      "root-folder/series-2/instance3.dcm", 
      "root-folder/series-2/instance2.dcm"
    ]
  }
]
```

### 3D DICOM Study

The following items list will create 1 task containing 2 series.

```json
[
  {
    "name": "study01",
    "items": [
      "study01/series01/instance01.dcm",
      "study01/series01/instance02.dcm",
      "study01/series01/instance03.dcm",
      "study01/series02/instance01.dcm",
      "study01/series02/instance02.dcm",
      "study01/series02/instance03.dcm",         
    ]
  },
]
```

## NIfTI Items List

### NIfTI Series

The following items list create two tasks, each with 1 series.

```json
[
  {
    "name": "series-001", // this is user defined
    "items": [
      "root-folder/series-1.nii"
    ]
  },
  {
    "name": "series-2",
    "items": [
      "root-folder/series-2.nii.gz"
    ]
  }
]
```

### NIfTI Study

The following items list will create two tasks, each with two series.&#x20;

```json
[
  {
    "name": "study01", 
    "items": [
      "study01/series01.nii",
      "study01/series02.nii"
    ]
  },
  {
    "name": "study02", 
    "items": [
      "study02/series01.nii",
      "study02/series02.nii"
    ]
  },
]
```

## Video Items List

The items list for importing images into the RedBrick AI platform is slightly different than images. Videos have to be parsed into frames and be imported into the RedBrick AI platform. Say you have two videos - `video1`, `video2`, that you want to import into the platform, and each video has three frames - `frame1.png`, `frame2.png`, `frame3.png`. The items list for this would be.

```javascript
[
  {
    "name": "video-1",
    "items": [
      "root-folder/video-1/frame1.png", // Your frames must be in correct order
      "root-folder/video-1/frame2.png",
      "root-folder/video-1/frame3.png",
    ]
  },
  {
    "name": "video-2",
    "items": [
      "root-folder/video-2/frame1.png",
      "root-folder/video-2/frame2.png",
      "root-folder/video-2/frame3.png",
    ]
  }
]
```

Using this items list, two video data points (video1, video2) will be imported into the platform with three frames each. The frames of each video will be ordered in the same order as their appearance in the items list.

## 2D Image Items List

The items list for importing images into the RedBrick AI platform is simply a list of item list entries. Each entry will be a single datapoint on the RedBrick AI platform. The item list below will import three data points into the RedBrick AI platform.

```javascript
  [
    {
      "items": ["root-folder/sub-folder/image1.png"] 
    },
    {
      "items": ["root-folder/sub-folder/image2.png"] 
    },
    {
      "items": ["root-folder/sub-folder/image3.png"] 
    }
  ]
```

