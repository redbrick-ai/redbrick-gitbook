# NIfTI Segmentations

{% embed url="https://www.loom.com/share/35707219702e44c383760839fd74d9cc?t=0" %}

This section of the documentation covers how you can upload NIfTI annotations along with DICOM/NIfTI images. Before following this guide, make sure to [set up the credentials for the CLI](../#create-a-credentials-config).

First, you need to either [clone an existing project](../#clone-an-existing-project), or [create a new project](../#create-a-project) with the CLI. Once you do this, make sure you enter your project's directory.

```
cd project-directory
```

{% hint style="warning" %}
You have to upload your Images and Annotation files together. To add annotation files to data you have already uploaded, please see [this](../../sdk-overview/label-and-review.md#programmatically-label).
{% endhint %}

## Upload cloud stored annotations

You can upload cloud stored annotation files along with your data. Your image data can be stored either locally or in the cloud as well - please have a look at the [importing data](../importing-data/) documentation for an overview of image data upload.&#x20;

### Configure cloud storage

First, you need to [configure your cloud storage bucket](../../../importing-data/configuring-external-storage/) with the appropriate permissions (PUT and GET access), so that RedBrick AI can read and write annotations from it.

### Set project label storage location

Next, you need to set your project's annotation storage method to your cloud storage. This is a project wide setting, and doing so will prompt RedBrick AI to read and write all annotations from your bucket.&#x20;

{% hint style="warning" %}
Once you set your projects annotation storage method, changing/deleting files in your cloud console can cause issues with your RedBrick AI projects. RedBrick AI will expect to find the annotation files in your bucket.
{% endhint %}

```
// Inside your project-directory
redbrick info set labelstorage
> Storage ID: <storage_id>
> Path prefix: path/to/label/directory
```

`<storage_id>` is a unique ID for your cloud storage method that can be found within the Storage Methods tab.&#x20;

`Path prefix` is the directory in your cloud bucket, within which your annotation files are. **Note - the file paths in the `segmentation` entry of your items list will be relative to this path.** You can leave it as the root of your bucket by defining it as `.`.

### Upload items list

To upload cloud stored annotations, you need to create an items file that provides details about your image data, annotation files, and annotation categories. You can find the format of this items list in the [Format Reference](../../reference/annotation-format-nifti.md#items-json). Here is a sample file:

```json
[
  {
    "items": ["series01.nii"],
    "name": "series01",
    "segmentations": ["series01_seg.nii"],
    "segmentMap": {
      "1": "taxonomy-category-1",
      "2": "taxonomy-cateogry-2"
    }
  },
  {
    "items": ["series02.nii"],
    "name": "series02",
    "segmentations": ["series02_seg.nii"],
    "segmentMap": {
      "1": "taxonomy-category-1",
      "3": "taxonomy-cateogry-3"
    }
  }
]
```

The following command will upload your annotation files (stored in `<storage_id>` set above), and your image files (stored in `<image_storage_id>`):

```
redbrick upload path/to/items.json --json --storage <image_storage_id>
```

{% hint style="info" %}
`--storage <image_storage_id>` is needed for cloud stored image data. Please have a look at [this documentation](../importing-data/direct-upload-to-redbrick.md) for uploading locally stored image data.
{% endhint %}

## Upload local annotations to RedBrick AI

You can upload NIfTI annotations along with either locally stored or cloud stored image data. The process of uploading locally stored annotations is similar to [cloud stored annotations](nifti-segmentations.md#configure-cloud-storage), except the file paths in your items file are absolute local paths to your annotation files. Here is an example items file:&#x20;

```json
[
  {
    "items": ["/local/path/to/series01.nii"],
    "name": "series01",
    "segmentations": ["/local/path/to/series01_seg.nii"],
    "segmentMap": {
      "1": "taxonomy-category-1",
      "2": "taxonomy-cateogry-2"
    }
  },
  {
    "items": ["/local/path/to/series02.nii"],
    "name": "series02",
    "segmentations": ["/local/path/to/series02_seg.nii"],
    "segmentMap": {
      "1": "taxonomy-category-1",
      "3": "taxonomy-cateogry-3"
    }
  }
]
```

```
// Inside your project directory
redbrick upload path/to/data --json
```

Running this command will prompt the CLI to recursively search the `data` folder for a `.json` file. Once it finds the `.json` file, it will use the mapping information within the file to upload the data.

{% hint style="info" %}
If your image data is stored in the cloud please have a look at [this documentation](../importing-data/items-list-for-cloud-data.md) for an overview on importing cloud image data.
{% endhint %}
