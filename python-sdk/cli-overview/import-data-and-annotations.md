# Import Data & Annotations

You can easily import large amounts of data from the command line interface. Before following this guide, make sure to [set up credentials for the CLI](./).

### Importing Locally Stored Data

Make sure your data is stored within the correct folder structure as [defined in our documentation](../../importing-data/direct-data-upload.md). You can only upload a single data type in one upload operation - see the [supported file types here](../../importing-data/direct-data-upload.md).

```bash
$ redbrick upload path/to/data/ --type DICOM3D
```

{% hint style="info" %}
You can see all of the available [types in the CLI upload reference documentation](https://redbrick-sdk.readthedocs.io/en/stable/cli.html#Positional%20Arguments\_repeat8).
{% endhint %}

#### Group Images by Study

To group your images by study (see [here for examples](../../importing-data/direct-data-upload.md)), input the following:&#x20;

```bash
$ redbrick upload path/to/data/ --as-study
```

#### Upload Video Frames

To upload a [video by uploading individual frames](../../importing-data/direct-data-upload.md#video-frames), input the following:

```
$ redbrick upload path/to/videoframes/ --as-frames --type VIDEOFRAMES
```

### Importing Externally Stored Data

To import data that is stored externally, (e.g. in an AWS s3 bucket), you must specify the storage ID. You can find your storage solution's unique Storage ID in the _Storage tab_ of the RedBrick AI platform.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-18 at 2.59.17 PM.png" alt=""><figcaption><p>Click on the field in order to copy the value to your clipboard.</p></figcaption></figure>

</div>

Prepare an [Items List](../../importing-data/import-cloud-data.md#items-list) containing references to your externally stored files.

```bash
$ redbrick upload items.json --storage STORAGEID # replace STORAGEID with your Storage ID
```

## Import Annotations

To import annotations with your data, you must create an [Items List](../../importing-data/import-cloud-data/creating-an-items-list.md) that contains annotation information in the proper [annotation format](../format-reference.md).

{% hint style="warning" %}
Please note that you can only import an Items File that contains annotations **using the SDK & CLI**. The RedBrick AI UI **does not support** importing JSON Items Files that contain annotations.
{% endhint %}

{% hint style="info" %}
The file paths within the Items List can point to locally stored data or data in your [external storage](../../importing-data/import-cloud-data/creating-an-items-list.md). \
\
If your image data is stored externally, be sure to provide the Storage ID with `--storage.`If your annotation files are stored externally, be sure to provide the Storage ID with `--label-storage.`
{% endhint %}

Here is a sample Items List that contains annotation information:&#x20;

{% code lineNumbers="true" %}
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
{% endcode %}

#### Import Locally Stored Annotations with Locally Stored Images

```bash
$ redbrick upload path/to/items.json # items.json must have local file paths.
```

#### Import Locally Stored Annotations with Externally Stored Images

The following command will upload your (locally stored) annotation files and your image files (stored in `STORAGEID`):

```bash
$ redbrick upload path/to/items.json --storage STORAGEID
```

#### Import Externally Stored Annotations and Externally Stored Images

If your annotation files are also stored externally, you can run the following command:&#x20;

```
$ redbrick upload path/to/items.json --storage STORAGEID --label-storage LABELSTORAGEID
```

### GitHub Example

You can follow along with this Jupyter notebook to upload the Brain Brats data along with its annotations.&#x20;

{% embed url="https://github.com/redbrick-ai/redbrick-examples/blob/main/DataIO/study-data-segmentation/main.ipynb" %}
