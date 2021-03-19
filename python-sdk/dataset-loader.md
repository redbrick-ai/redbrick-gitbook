---
description: >-
  The dataset loader is an interface similar to Datapoint Creator. It is useful
  to upload batches of data with or without labels in a single call to the
  backend using json files.
---

# Dataset Loader

## Overview

```python
redbrick.dataset.DatasetLoader(
    org_id: str, 
    data_set_name: str
)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Description |
| :--- | :--- |
| `org_id` | Your organization id, can be found in the url `https://app.redbrickai.com/<org_id>/` |
| `data_set_name` | The name of the dataset to store this datapoint to. |
{% endtab %}

{% tab title="Methods" %}
### Upload Items

Uploads a list of items to the dataset.

```python
upload_items(
    items: str, 
    storage_id: str
)
```

| Parameter | Description |
| :--- | :--- |
| `items` | File path to json file containing items data. |
| `storage_id` | Storage method id. Can be found on _**Data Warehouse -&gt; Storage**_ |

### Upload Items with Labels

Uploads a list of items along with its corresponding labels to the dataset and labelset provided.

```python
upload_items_with_labels(
    items: str, 
    storage_id: str,
    label_set_name: str, 
    task_type: str
)
```

| Parameter | Description |
| :--- | :--- |
| `items` | File path to json file containing items data with labels. |
| `storage_id` | Storage method id. Can be found on _**Data Warehouse -&gt; Storage**_ |
| `label_set_name` | Name of label set to upload labels to. |
| `task_type` | Type of labeling task. IE: "BBOX" |
{% endtab %}
{% endtabs %}

## Usage

**Creating a DatasetLoader reference**

To create a DatasetLoader object, you need to do the following.

```python
import redbrick
from redbrick.dataset import DatapointCreator

redbrick.init(api_key="<your_api_key>")
ds_loader = DatasetLoader(
        org_id="<org_id>", 
        data_set_name="<data_set_name>"
    )
```

The organization id is available from the URL when you're logged into the platform - `https://app.redbrickai.com/<org_id>/`

**Uploading a list of items with labels**

To upload a list of items with labels you can use the following code, please note that the used variables are only for demonstration purposes:

```python
json_datafile_labeled = "itemslabeled.json"
fakeStorageId = "0f03e746-0997-41c5-a411-ab5cfb966c21"
fakeLabelsetName = "Testing Labelset"
task_type_ = "BBOX"

ds_loader.upload_items_with_labels(
    items=json_datafile_labeled,
    storage_id=fakeStorageId,
    label_set_name=fakeLabelsetName,
    task_type=task_type_
)
```

