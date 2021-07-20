---
description: Programmatically exporting data from your RedBrick AI Project.
---

# Export

## RedBrick Format

The `redbrick_format()` method allows you to export your labels in the custom RedBrick AI format. 

```python
result = project.export.redbrick_format()
```

**`result`** _returned value_  
The result export format is shown below, where `LabelObject` is defined in the [reference documentation.](reference.md)

```javascript
[
  {
    "name": "image_name", // same unique name used on upload
    "items": ["image/url.png"], // image url, or frame urls
    "itemsPresigned": ["image/url_presigned.png"], // same as above, but signed urls
    "createdBy": "email@email.com",
    "dpId": "123", // unique id assigned to each datapoint

    "labels": [LabelObject]
  }
]
```

## Coco Format

The `coco_format()` method exports your data in the coco format. Please refer to the [official documentation](https://cocodataset.org/#format-data) for an overview of the COCO documentation.

```python
result = project.export.coco_format()
```

{% hint style="warning" %}
Coco export will only work for Bounding box and Polygon labeling projects. 
{% endhint %}

## Code Example

```python
import json
import redbrick

# Standard Setup
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
project = redbrick.get_project(api_key, url, org_id, project_id)

# Get all data
result = project.export.redbrick_format()

# Write to file
with open("redbrick_export.json", "w+") as file_:
    json.dump(result, file_, indent=2)
```



