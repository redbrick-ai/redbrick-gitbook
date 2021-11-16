---
description: Programmatically uploading data to your RedBrick AI Project.
---

# Upload

## Create Datapoints

The `create_datapoints` function allows you to programmatically upload your data and labels to your RedBrick AI project.&#x20;

```python
failed_to_create = project.upload.create_datapoints(
                       storage_id, datapoints, is_ground_truth=False
                   )
```

**`storage_id: str` **

This is a unique ID that defines your [RedBrick AI storage method](../projects/importing-data/#storage-methods). For external storage methods, you can find the ID on the Storage Method tab on the platform. There are two special storage methods that you can use:&#x20;

1. `redbrick.StorageMethod.PUBLIC`. Public storage methods allow you to upload URL's to RedBrick that reference publicly stored data. &#x20;
2. `redbrick.StorageMethod.REDBRICK`. RedBrick storage allows you to perform `Direct Upload` through the SDK . When you use the RedBrick Storage, you items paths must be valid paths to locally stored data.&#x20;

**`datapoints: List[Dict]` **\
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

**`is_ground_truth: bool`**

Optional, False by default. Setting this value to True will upload the task directly into the ground truth state at the end of your pipeline. This can be useful for performing active learning with data you already have labeled.

## Create Datapoints with Masks

The `create_datapoint_from_masks` function allows you to programmatically upload your data with mask labels. This function uploads only a single datapoint with a mask, you'll have to call it once for every image/label you upload.&#x20;

{% hint style="info" %}
`create_datapoint_from_masks` will only work with `SEGMENATION` type projects. To upload labels of different types, please use the `create_datapoints` function. &#x20;
{% endhint %}

```python
failed_to_create = project.upload.create_datapoint_from_mask(
                       storage_id, mask, class_map, image_path
                   )
```

**`storage_id: str` **

This is a unique ID that defines your [RedBrick AI storage method](../projects/importing-data/#storage-methods). For external storage methods, you can find the ID on the Storage Method tab on the platform. There are two special storage methods that you can use:&#x20;

1. `redbrick.StorageMethod.PUBLIC`. Public storage methods allow you to upload URL's to RedBrick that reference publicly stored data. &#x20;
2. `redbrick.StorageMethod.REDBRICK`. RedBrick storage allows you to perform `Direct Upload` through the SDK . When you use the RedBrick Storage, you items paths must be valid paths to locally stored data.&#x20;

**`mask: np.ndarray`**

The mask you want to upload in the form of a Numpy Array with dimensions `(m, n, 3)` where the channels are RGB. The numpy array must be of type `np.uint8.`&#x20;

**`class_map: Dict[str, List[int]]`**

The class map object must contain a mapping from the category and the corresponding RGB color. This object needs to be in the same format as the file that gets exported by RedBrick. Please see the [reference](reference.md#png-mask-formats).&#x20;

**`image_path: str`**

If you are using external storage, this needs to be your [items path](../projects/importing-data/#items-list). If using `redbrick.StorageMethod.REDBRICK` i.e. Direct Upload, this needs to be the path to your locally stored data. &#x20;



## Code Example

{% hint style="success" %}
Please look at the [overview](sdk-overview.md#getting-started) to understand how to do the Standard Setup.
{% endhint %}

### **create\_datapoints**

```python
import redbrick

# Standard set up
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
project = redbrick.get_project(api_key, url, org_id, project_id)

# default public storage method
storage_id = redbrick.StorageMethod.PUBLIC
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

### create\_datapoint\_from\_mask

```python
"""Uploads images/masks that were exported from RedBrick."""
import redbrick
from PIL import Image
import numpy as np

# Standard set up
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
project = redbrick.get_project(api_key, url, org_id, project_id)

dir = "<TODO>" # directory containing the exported data

with open(os.path.join(dir, "class_map.json"), "r") as file:
    class_map = json.load(file)
with open(os.path.join(dir, "datapoint_map.json"), "r") as file:
    datapoint_map = json.load(file)

# iterate over files, and upload data with masks. 
for file in datapoint_map:
    mask_im = Image.open(os.path.join(dir, file))
    mask = np.array(mask_im)[:, :, 0:3] # Ignore Alpha channel
    mask = mask.astype(np.uint8)
    
    # because we are using redbrick.StorageMethod.REDBRICK, 
    # the image_path will need to be path to a locally stored image. 
    image_path = datapoint_map[file]
    project.upload.create_datapoint_from_masks(
        redbrick.StorageMethod.REDBRICK, mask, class_map, image_path
    )
```
