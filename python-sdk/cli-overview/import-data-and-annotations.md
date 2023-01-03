# Import data & annotations

You can use the command line interface to easily import large amounts of data. Before following this guide, make sure to [set up credentials for the CLI](./).

### Importing locally stored data

Make sure your data is stored within the correct folder structure as [defined in our documentation](../../importing-data/direct-data-upload.md). You can only upload a single data type in one upload operation - see the [supported file types here](../../importing-data/direct-data-upload.md).

```bash
$ redbrick upload path/to/data/ --type DICOM3D
```

{% hint style="info" %}
See all the [types in the CLI upload reference documentation](https://redbrick-sdk.readthedocs.io/en/stable/cli.html#Positional%20Arguments\_repeat8).
{% endhint %}

#### Group images by study

To group your images by study (look [here for examples](../../importing-data/direct-data-upload.md)), do the following:&#x20;

```bash
$ redbrick upload path/to/data/ --as-study
```

#### Upload video frames

To upload a [video by uploading individual frames](../../importing-data/direct-data-upload.md#video-frames), do the following:

```
$ redbrick upload path/to/videoframes/ --as-frames --type VIDEOFRAMES
```

### Importing externally stored data

To import data stored externally, for example in AWS s3, you must specify the storage ID (you can get your storage systems storage ID from the _Storage tab_ on the RedBrick AI platform).&#x20;

Make sure to prepare an [Items List](../../importing-data/import-cloud-data.md#items-list) containing references to your externally stored files.

```bash
$ redbrick upload items.json --storage STORAGEID # replace STORAGEID with your Storage ID
```

## Import annotations

To import annotations with your data, you must create an [Items List](broken-reference) that contains annotation information in the [annotation format](../reference/annotation-format.md).

{% hint style="warning" %}
Please note that you can only import an Items File containing annotations using the SDK & CLI. We do not support importing JSON Items Files through the UI.
{% endhint %}

{% hint style="info" %}
The file paths within the Items List can point to locally stored data or data in your [external storage](../../importing-data/configuring-external-storage/). \
\
If your image data is stored externally, make sure to provide the Storage ID with `--storage.`If your annotation files are stored externally, make sure to provide the Storage ID with `--label-storage.`
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

#### Import locally stored annotations with locally stored images

```bash
$ redbrick upload path/to/items.json # items.json must have local file paths.
```

#### Import locally stored annotations with externally stored images

The following command will upload your annotation files (stored locally), and your image files (stored in `STORAGEID`):

```bash
$ redbrick upload path/to/items.json --storage STORAGEID
```

#### Import externally stored annotations and externally stored images

If you annotation files are also stored externally, you can run the following:&#x20;

```
$ redbrick upload path/to/items.json --storage STORAGEID --label-storage LABELSTORAGEID
```

### GitHub example

You can follow along with this Jupyter notebook to upload the Brain Brats data along with the annotations.&#x20;

{% embed url="https://github.com/redbrick-ai/redbrick-examples/blob/main/DataIO/study-data-segmentation/main.ipynb" %}
