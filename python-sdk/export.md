---
description: >-
  The export module provides a way to export both your data and labels to your
  local machine with little effort.
---

# Export

## Overview

```python
redbrick.export.Export(org_id: str, label_set_name: str, target_dir: str)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Description |
| :--- | :--- |
| `org_id` | Your organization id, can be found in the url `https://app.redbrickai.com/<org_id>/` |
| `label_set_name` | The name of the labelset that you want to export |
| `target_dir` | Directory where you want to store your data and labels. |
{% endtab %}

{% tab title="Methods" %}
```
export(
    download_data: bool, 
    single_json: bool, 
    use_name: bool, 
    export_format: str
)
```

| Parameter | Description |
| :--- | :--- |
| `download_data` | Boolean flag to download image/video data to local folder. Default: **False**. |
| `single_json` | Boolean flag to store all datapoint labels in a single json file. Default: **False** |
| `use_name` | Boolean flag to use datapoint name instead of datapoint id as filename for json and image data. Default: **False** |
| `export_format` | String to indicate which format should be used at export time. If task is image segmentation and want to output masks, you should use **"png"**; all other cases must be **"redbrick"**. Default: **"redbrick"**  |

|  |  |
| :--- | :--- |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**For new projects \(created after Jun 20 2021, or** [**without the deprecated tag**](../product-updates/june-2021.md#datasets-and-labelsets-moved-inside-projects) **on the header\).** 

Labelsets automatically get created for new projects, so you can export the data by using the following key in as the `labelset_name: project_id-output.` 
{% endhint %}

## Usage

**Creating an Export reference**

To create an Export object, you need to do the following.

```python
import redbrick
from redbrick.export import Export

redbrick.init(api_key="<your_api_key>")
export_rb = Export(
        org_id="<org_id>", 
        label_set_name="<label_set_name>", 
        target_dir="<target_dir>"
    )
```

The organization id is available from the URL when you're logged into the platform - `https://app.redbrickai.com/<org_id>/`

**Exporting your data and labels**

To export your data and labels, you can do the following:

```python
export_rb.export(download_data=True, single_json=True)
```

\*\*\*\*

