# Importing data

The data that you use with the RedBrick AI platform can be stored in a number of places, you can upload data directly to the platform or integrate an external storage method to store your data like Amazon S3, Google Cloud Platform, or Azure Blob Storage. By using your own external storage method, you can manage the storage of your raw data, including granular level access and privacy control.

You can see the external storage method data model on the RedBrick AI model. When data is stored externally, your raw data will never be routed via RedBrick AI servers, nor will it be downloaded/duplicated (unless specifically requested for certain features, please review our [Privacy Policy](https://redbrickai.com/policies/privacy.pdf)). The data is transferred directly from your storage method to your browser.&#x20;

![RedBrick AI external storage data model.](../../.gitbook/assets/group-476.png)

## Using external storage involves two steps

1. Configuring your [Storage Method](./#storage-methods) to specify data storage locations, and authentication information.&#x20;
2. Uploading an [Items List](./#uploading-an-items-list) containing specific URL's of the data from your storage method you wish to import.&#x20;

## Configure a Storage Method

Currently, the options for external Storage Methods are:

* [AWS S3 Buckets](configuring-aws-s3-storage.md).
* [Google Cloud Storage.](configuring-google-cloud-storage.md)
* [Azure Blob Storage.](broken-reference)
* [Public](public-storage.md). This storage type includes data stored on your computer and data stored on any public server accessible by a URL.&#x20;
* [Direct Upload](direct-upload.md). This storage type allows you to store your data securely on RedBrick AI servers without having to configure your own storage method.

You can create a storage method by clicking on the **Storage Method **_****_ on the left side bar of your account. On the storage method page, click on **Create Storage Method**. _****_&#x20;

## Upload an Items List to Your Project

{% hint style="info" %}
For [Direct Upload](direct-upload.md) i.e. uploading your image files directly to RedBrick AI servers, you don't have to create an items list.&#x20;
{% endhint %}

The items list points the RedBrick AI platform to the data points in the data storage. This way you can selectively import data points from a storage method. Once you create your JSON items list, you can upload it through the UI, or [SDK](../../python-sdk/sdk-overview/importing-data-and-labels.md#creating-data-points-without-labels).

![Upload your items list from the project dashboard](<../../.gitbook/assets/Screen Shot 2022-02-23 at 3.19.08 PM.png>)

![Select your Storage Method type, and upload your items file](<../../.gitbook/assets/Screen Shot 2022-02-23 at 3.20.56 PM.png>)

## Items List Format&#x20;

The items list is a JSON file which comprises of a list of entries of the following format.

```javascript
{
    "items": ["<filepath_of_datapoint>"]
    "name": "<name_of_datapoint>" // Needs to be unique
                                  // Required for videos & DICOM, 
                                  // optional for images
}
```

{% hint style="info" %}
Please visit the relevant documentation to see the format of the `items` path for each of the storage methods:&#x20;

* [AWS s3 items path](configuring-aws-s3-storage.md#items-path)
* [Azure Blob items path](configuring-azure-blob-storage.md#items-path)
* [Google Cloud Storage items path](configuring-google-cloud-storage.md#items-path)
* [Public Storage items path](public-storage.md#items-path)
{% endhint %}

### Image Items List

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

### Video Items List

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

### DICOM Series Import

To import multiple DICOM series, you need to create an items list of the following format:&#x20;

```json
[
  {
    "name": "series-001", // this is user defined
    "items": [
      "root-folder/series-1/instance1.dcm",
      "root-folder/series-1/instance2.dcm",
      "root-folder/series-1/instance3.dcm",
    ]
  },
  {
    "name": "series-2",
    "items": [
      "root-folder/series-2/instance1.dcm", // The instances don't need to be
      "root-folder/series-2/instance3.dcm", // in correct order.
      "root-folder/series-2/instance2.dcm",
    ]
  }
]
```

This Items list would import two series, with 3 instances each.&#x20;



### NIfTI Import

To import NIfTI files stored on your private storage method, you need to create an items list of the following format:

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

The above items list will create 2 separate tasks, 1 for each scan.

The RedBrick AI interface supports both compressed (gzipped) and uncompressed NIfTI files.&#x20;

You can also upload NIfTI files directly through the UI.&#x20;
