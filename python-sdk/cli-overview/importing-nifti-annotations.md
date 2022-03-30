# Importing NIfTI annotations

This section of the documentation covers how you can upload NIfTI annotations along with DICOM/NIfTI images. Before following this guide, make sure to [set up the credentials for the CLI](./#create-a-credentials-config).

First, you need to either [clone an existing project](./#clone-an-existing-project), or [create a new project](./#create-a-project) with the CLI. Once you do this, make sure you enter your project's directory.

```
cd project-directory
```

{% hint style="warning" %}
Make sure the data type you are uploading matches the data type of the project you are uploading into. For example, DICOM and NIfTI files can only be uploaded within DICOM projects.&#x20;
{% endhint %}

## Preparing your data files

You can upload NIfTI annotations along with either NIfTI images or DICOM images. The first thing you will need is all your image files, and corresponding annotation files. Say you have data in the following structure:&#x20;

```bash
data
├── items.json // Contains mapping information
├── annotations // Stores annotation NIfTI files
│   └── patient01
│       └── study01
│           ├── series01
│           │   └── segmentation.nii.gz
│           └── series02
│               └── segmentation.nii.gz
└── images // Stores DICOM/NIfTI image files
    └── patient01
        └── study01
            ├── series01
            │   ├── instance01.dcm
            │   ├── instance02.dcm
            │   └── instance03.dcm
            └── series02
                └── series.nii.gz
```

In above structure, I have a mix of DCM and NIfTI files in my images folder, and corresponding NIfTI annotation files.&#x20;

{% hint style="info" %}
You don't have to store your data in the structure above. We're just using this as an example for the documentation.
{% endhint %}

Once you have your data prepared, our platform needs two key pieces of information (which is provided in the items.json file) to correctly upload the data:&#x20;

1. The mapping between image file(s) and annotation file.&#x20;
2. The mapping between class Id's in the NIfTI annotation matrix and your [Taxonomy](../../data-labeling/taxonomies.md) category names.&#x20;

### Creating your Items file

The items file has the following format:

```json
[
    {
      "items": ["images/patient01/study01/series02/series.nii.gz"],
      "labelsPath": "annotations/patient01/study01/series02/series.nii.gz",
      "labels": [
        {
          "category": [["object", "taxonomy-category-1"]],
          "attributes": [],
          "dicom": { "instanceid": 1 }
        },
        {
          "category": [["object", "taxonomy-category-2"]],
          "attributes": [],
          "dicom": { "instanceid": 2 }
        }
      ]
    }
]
  
```

* `items`: Relative path (from the `items.json` file) to your images. In the case of a DICOM series, this will be a list of all the `.dcm` files in the series.&#x20;
* `labelsPath`: Relative path (from the `items.json` file) to your annotation for the image.&#x20;
* `labels`: A list of objects defining the mapping between Taxonomy category and NIfTI annotation instance id.
  * `category`: Your taxonomy category name `[["object", "replace-this-with-your-category-name"]].`
  * `attributes`: A list of Taxonomy attributes for this task.
  * `dicom`: The instance ID corresponding to the `category.`

## Uploading the data and annotations

Make sure you are within your project directory

```
cd project-directory
```

Upload the data with the `--json` parameter

```
redbrick upload path/to/data --json
```

Running this command will prompt the CLI to recursively search the `data` folder for a `.json` file. Once it finds the `.json` file, it will use the mapping information within the file to upload the data.&#x20;

{% hint style="info" %}
If you want to upload data from your [external storage](../../projects/importing-data/), the path to your data in your `items.json` file will need to be relative paths within your storage method. \
\
You will also need to specify the storage method you wish to use. In this case, your `data/` folder can contain only your `items.json` file.&#x20;

`redbrick upload path/to/data --json --storage YOUR_STORAGE_ID`.
{% endhint %}

