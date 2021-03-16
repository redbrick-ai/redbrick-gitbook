# Labelset \(deprecated\)

The labelset module gives you programmatic access to the labelsets within your organization. Using the labelset module, you can export labels in various formats, read the data into memory, or inspect the labels.

{% hint style="warning" %}
The Labelset module is deprecated and actively supported only for versions **0.2.16** and before. To export your labels with newer version of the RedBrick SDK, please use the [Export module](../export.md).
{% endhint %}

## Overview

```python
redbrick.labelset.LabelsetLoader(org_id: str, label_set_name: str)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Description |
| :--- | :--- |
| `org_id` | Your organization id, can be found in the url `https://app.redbrickai.com/<org_id>/` |
| `label_set_name` | The name of the labelset that you |
| `task_type` | The type of labels in this labelset e.g. `BBOX`, `CLASSIFY` |
| `data_type` | The type of data in this labelset e.g. `IMAGE`, `VIDEO` |
{% endtab %}

{% tab title="Methods" %}
| Method | Description |
| :--- | :--- |
| `export(format: str)` | Exports your data and labels in the specified format, Look at exporting your data and labels section for details on the formats. |
{% endtab %}
{% endtabs %}

## Usage

**Creating a labelset reference**

To create a labelset object, you need to do the following.

```python
import redbrick

redbrick.init(api_key="<your_api_key>")
label_set = redbrick.labelset.LabelsetLoader(
    org_id = "<org_id>", label_set_name="<label_set_name>"
)
```

The organization id is available from the URL when you're logged into the platform - `https://app.redbrickai.com/<org_id>/`

**Exporting your data and labels**

To export your data and labels, you can do the following:

```python
label_set.export(format="<format>")
```

Where format specifies the export format, and can take the following values:

| Data Type | Label Type | Formats |
| :--- | :--- | :--- |
| `IMAGE` | Bounding Box | `redbrick`,`yolo` |
|  | Segmentation | `redbrick`,`redbrick-png` |
|  | Polygon | `redbrick` |
|  | Polyline | `redbrick` |
|  | Keypoint | `redbrick` |
|  | Ellipse | `redbrick` |
|  | Classification | `redbrick` |
| `VIDEO` | Bounding Box | `redbrick`,`yolo` |
|  | Classification | `redbrick`,`redbrick-json` |

**Visualizing image data and labels**

You can visualize random labels rendered on image data by doing the following.

```text
label_set.show_data()
```

