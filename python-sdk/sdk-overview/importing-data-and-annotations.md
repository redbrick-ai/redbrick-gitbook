# Importing data & annotations

You can programmatically import data and/or annotations using the SDK with a Python Script. For simple import operations, we recommend using the CLI, which has a simple & optimized interface.&#x20;

You can import either locally stored data or externally stored data using the SDK using `create_datapoints`.

{% hint style="success" %}
Please see the full reference documentation for [`create_datapoints` here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.upload.Upload.create\_datapoints).
{% endhint %}

Perform the [standard RedBrick AI SDK set-up](./#initializing-the-redbrick-sdk-in-python) to create a project object.

```python
project = redbrick.get_project(org_id, project_id, api_key)
```

#### Import locally stored data

To import locally stored data, create a list of `points` with relative file paths to your locally stored data, and use the [`redbrick.StorageMethod.REDBRICK`](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.StorageMethod) storage ID.&#x20;

```python
points = [{"items": ["path/to/data.nii"], "name": "..."}]
storage_id = redbrick.StorageMethod.REDBRICK

project.upload.create_datapoints(storage_id=storage_id, points=points)
```

{% hint style="info" %}
Please visit the [Items List](../../importing-data/import-cloud-data/#items-list) documentation to understand the format of the `points` array.
{% endhint %}

#### Import externally stored data

To import data stored in an external storage method, like AWS s3, make sure to use the storage methods Storage ID found on the _Storage_ tab of your RedBrick AI account.

#### Import annotations

If you want to upload annotations with your data, include the annotation information in the `points` object.

```python
points = [
    {
        "name": "...",
        "series": [
            {
                "items": "path/to/data.nii",
                "segmentation": "path/to/segmentation.nii",
                "segmentMap": {1: "category-1", 2: "category-2"},
            }
        ],
    }
]
project.upload.create_datapoints(storage_id="...", points=points)
```

{% hint style="info" %}
Please visit our [annotation format reference](../reference/annotation-format.md) to understand the format of the annotations.
{% endhint %}
