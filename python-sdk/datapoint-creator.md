---
description: >-
  The datapoint creator is an interface to programmatically upload datapoint
  data (just images or images with labels) to the RedBrick AI Data Warehouse.
---

# Datapoint Creator

## Overview

```python
redbrick.dataset.DatapointCreator(
    org_id: str, 
    data_set_name: str, 
    storage_id: str, 
    label_set_name: str = None
)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Description |
| :--- | :--- |
| `org_id` | Your organization id, can be found in the url `https://app.redbrickai.com/<org_id>/` |
| `data_set_name` | The name of the dataset to store this datapoint to. |
| `storage_id` | Storage method id. Can be found on _**Data Warehouse -&gt; Storage**_ |
| `label_set_name` | **Optional**. The name of the labelset to store this datapoint to. If set, then a list of labels must be passed when calling _**create\_datapoint**_ method. |
{% endtab %}

{% tab title="Methods" %}
```python
create_datapoint(
    name: str, 
    items: List[str], 
    labels: List[Dict] = None
)
```

| Parameter | Description |
| :--- | :--- |
| `name` | Name of current datapoint. |
| `items` | List of strings containing URLs to image data. Single URL if Image data; multiple URLs if Video data. |
| `labels` | **Optional**. List of label dictionaries in redbrick format. If a **label set** **name** was passed to DatapointCreator object, then this parameter must be specified. |
{% endtab %}
{% endtabs %}

## Usage

**Creating an DatapointCreator reference**

To create a DatapointCreator object, you need to do the following.

```python
import redbrick
from redbrick.dataset import DatapointCreator

redbrick.init(api_key="<your_api_key>")
dp_creator = DatapointCreator(
        org_id="<org_id>",
        data_set_name="<data_set_name>",
        storage_id="<storage_id>",
        label_set_name="<label_set_name>"
    )
```

The organization id is available from the URL when you're logged into the platform - `https://app.redbrickai.com/<org_id>/`

The storage id can be found on:`https://app.redbrickai.com/<org_id>/warehouse#storage`

**Creating a datapoint**

To create a datapoint you can use the following code, please note that the used variables are only for demonstration purposes:

```python
_name = "chevrolet"
_items = [
    "https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/Chevrolet_Onix_20150814-DSC05650.JPG/320px-Chevrolet_Onix_20150814-DSC05650.JPG"
]
_labels = [
    {
        "attributes": [],
        "category": [["object", "car"]],
        "labelid": "2",
        "bbox2d": {"xnorm": 0.1, "ynorm": 0.2, "wnorm": 0.8, "hnorm": 0.7},
    }
]

dp_creator.create_datapoint(
    name=_name, 
    items=_items, 
    labels=_labels
)
```

