---
description: Programmatically uploading data to your RedBrick AI Project.
---

# Upload

## Create Datapoints

The `create_datapoints` function allows you to programmatically upload your data and labels to your RedBrick AI project.&#x20;

```python
failed_to_create = project.upload.create_datapoints(storage_id, datapoints)
```

**`storage_id` **\
****Your RedBrick AI [storage method's](../projects/importing-data/#storage-methods) unique ID. Public storage methods have a default ID of `"11111111-1111-1111-1111-111111111111"`.

**`datapoints` **\
****The list of datapoints that you want to upload to the platform. See the `LabelObject` format in the [reference documentation](reference.md).

```python
[
    {
        "name": "my first upload", # unique for each datapoint
        "items": [
            "http://datasets.redbrickai.com/car-vids/car-1/frame20.png"
        ], # URL of the image, or video frames
        "labels": [LabelObject]
    }
]
```

## Create Datapoints from Masks

The `create_datapoints_from_masks` function allows you to programmatically upload your data with mask labels.&#x20;

{% hint style="info" %}
`create_datapoints_from_masks` will only work with `SEGMENATION` type projects. To upload labels of different types, please use the `create_datapoints` function. &#x20;
{% endhint %}

```
failed_to_create = project.upload.create_datapoints(storage_id, mask_dir)
```

**`storage_id` **\
****Your RedBrick AI [storage method's](../projects/importing-data/#storage-methods) unique ID. Public storage methods have a default ID of `"11111111-1111-1111-1111-111111111111"`.

**`mask_dir` **\
**** Path to the directory containing your masks and category information. Please see the [reference documentation](reference.md#png-mask-formats) for details about the required format for your masks directory.&#x20;

## Code Example

Get your storage methods storage id. If you haven't created a storage method, please look at the [documentation](../projects/importing-data/#using-external-storage-involves-two-steps). For this example we're using the default Public Storage (storage ID: "11111111-1111-1111-1111-111111111111" ) method which allows using public data accessible by a URL.

{% hint style="success" %}
Please look at the [overview](sdk-overview.md#getting-started) to understand how to do the Standard Setup.
{% endhint %}

```python
import redbrick

# Standard set up
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
project = redbrick.get_project(api_key, url, org_id, project_id)

# default public storage method
storage_id = "11111111-1111-1111-1111-111111111111"
datapoints = [
    {
        "name": "my first upload",
        "items": [
            "http://datasets.redbrickai.com/car-vids/car-1/frame20.png"
        ]
    }
]
failed_to_create = project.upload.create_datapoints(storage_id, datapoints)
```

{% hint style="info" %}
The easiest way to modify this script for your own use, would be to select some public URL's (for example from Google, or Flickr) and create your own custom `datapoint `object.
{% endhint %}

Check for any upload errors.

```python
failed_to_create = project.upload.create_datapoints(storage_id, datapoints)

for point in failed_to_create:
    print(point["error"])
```

