# Importing Data & Annotations

The RedBrick AI SDK allows you to programmatically import data and/or annotations with a Python script.&#x20;

For simple import operations, we recommend using the [CLI](https://docs.redbrickai.com/python-sdk/cli-overview/import-data-and-annotations).

You can import either locally or externally stored data via the SDK using the `create_datapoints` method.

{% hint style="success" %}
Please see the full reference documentation for [`create_datapoints` here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.upload.Upload.create\_datapoints).
{% endhint %}

#### Project Setup

Perform the [standard RedBrick AI SDK set-up](./#initializing-the-redbrick-sdk-in-python) to create a Project object.

```python
project = redbrick.get_project(org_id, project_id, api_key)
```

#### Import Locally Stored Data

To import locally stored data, create a list of `points` with relative file paths to your locally stored data, and use the [`redbrick.StorageMethod.REDBRICK`](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.StorageMethod) storage ID.&#x20;

```python
# create a list of file paths to your locally stored data
points = [{"items": ["path/to/data.nii"], "name": "..."}]

# designate the correct Storage Method (in this case, local)
storage_id = redbrick.StorageMethod.REDBRICK

# perform the upload operation
project.upload.create_datapoints(storage_id=storage_id, points=points)
```

{% hint style="info" %}
Please see the [Items List](../../importing-data/import-cloud-data.md#items-list) documentation for a comprehensive overview of the `points` array.
{% endhint %}

#### Import Externally Stored Data

To import data stored in an external storage method such as AWS s3, be sure to use the Storage ID found on the _Storage_ tab of your RedBrick AI account.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-18 at 2.59.17 PM.png" alt=""><figcaption><p>Click on the field to copy the Storage ID to your clipboard!</p></figcaption></figure>

</div>

#### Import Annotations

If you want to upload annotations with your data, include `segmentations` and `segmentMap` annotation information in the `points` object.

```python
points = [
    {
        "name": "...",
        "series": [
            {
                "items": "path/to/data.nii",
                
                # path to your annotation file
                "segmentations": "path/to/segmentation.nii",
                
                # segment mapping of the annotation file (often viewed with nibabel)
                "segmentMap": {1: "category-1", 2: "category-2"},
            }
        ],
    }
]
project.upload.create_datapoints(storage_id="...", points=points)
```

{% hint style="info" %}
Please see our [annotation format reference](../format-reference.md) for a more detailed overview.
{% endhint %}
