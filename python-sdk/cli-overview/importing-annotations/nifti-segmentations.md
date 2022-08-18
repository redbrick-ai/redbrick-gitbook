# NIfTI Segmentations

{% hint style="info" %}
Please see this example script on GitHub for a complete overview of uploading annotations.
{% endhint %}

{% embed url="https://github.com/redbrick-ai/redbrick-examples/blob/main/DataIO/study-data-segmentation/main.ipynb" %}
Example Jupyter Notebook for importing annotations using the CLI
{% endembed %}

This section of the documentation covers how you can upload NIfTI annotations along with DICOM/NIfTI images. Before following this guide, make sure to [set up the credentials for the CLI](../#create-a-credentials-config).

First, you need to either [clone an existing project](../#clone-an-existing-project) or [create a new project](../#create-a-project) with the CLI. Once you do this, make sure you enter your project's directory.

```
cd project-directory
```

{% hint style="warning" %}
You have to upload your Images and Annotation files together. To add annotation files to data you have already uploaded, please see [this](../../sdk-overview/label-and-review.md#programmatically-label).
{% endhint %}

## Upload cloud-stored annotations

You can upload cloud-stored annotation files along with your data. Your image data can be stored either locally or in the cloud as well - please have a look at the [importing data](../importing-data/) documentation for an overview of image data upload.&#x20;

### Configure cloud storage

First, you need to [configure your cloud storage bucket](../../../importing-data/configuring-external-storage/) with the appropriate permissions (PUT and GET access), so that RedBrick AI can read and write annotations from it.

### Upload items list

To upload cloud-stored annotations, you need to create an items file that provides details about your image data, annotation files, and annotation categories. You can find the format of this items list in the [Format Reference](../../reference/annotation-format.md#items-json). Here is a sample file:

```json
[
  {
    "name": "study1",
    "series": [
      {
        "items": "series1.nii",
        "name": "series1",
        "segmentations": "series1_seg.nii"
      },
      {
        "items": "series2.nii",
        "name": "series2",
        "segmentations": "series2_seg.nii"
      }
    ],
    "segmentMap": {
      "1": {
        "category": "necrosis"
      },
      "2": {
        "category": "edema"
      },
      "3": {
        "category": "non-enhancing tumor"
      },
      "4": {
        "category": "enhancing tumor"
      }
    }
  },
  {
    "name": "study2",
    "series": [
      {
        "items": "series1.nii",
        "name": "series1",
        "segmentations": "series1_seg.nii"
      },
      {
        "items": "series2.nii",
        "name": "series2",
        "segmentations": "series2_seg.nii"
      }
    ],
    "segmentMap": {
      "1": {
        "category": "necrosis"
      },
      "2": {
        "category": "edema"
      },
      "3": {
        "category": "non-enhancing tumor"
      },
      "4": {
        "category": "enhancing tumor"
      }
    }
  },
]
```

#### Local annotations and Local images

```
redbrick upload path/to/items.json --json
```

#### Local annotations cloud images

The following command will upload your annotation files (stored locally), and your image files (stored in `<storage_id>`):

```bash
redbrick upload path/to/items.json --json --storage <storage_id>
```

#### Cloud annotations and cloud images

If your annotations are also stored in the cloud, you can run the following:

```bash
redbrick upload path/to/items.json --json --storage <storage_id> --label-storage <label_storage_id>
```
