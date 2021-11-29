# Exporting your data

Programmatically export your data with the RedBrick AI SDK in one of the following formats:&#x20;

1.  RedBrick AI Format.&#x20;

    See [reference](reference.md#redbrick-ai-export-format) documentation for overview of format.
2.  COCO Format.&#x20;

    Please see [COCO documentation](https://cocodataset.org/#format-data) for overview of format.
3.  Segmentation PNG masks.&#x20;

    See [reference](reference.md#png-mask-formats) documentation for overview of format.

### Code Example

Perform the standard RedBrick AI SDK set-up to create a RBProject object

```python
import redbrick

# Standard Setup
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)
```

#### Export in RedBrick AI Format

```python
# Export data in RedBrick AI Format
result = project.export.redbrick_format(only_ground_truth=True)

# Export all data with most recent labels, including datapoints
# that haven't been reviewed. 
result = project.export.redbrick_format(only_ground_truth=False)

# Export only a single task's labels. 
# Task id can be found in your project Data Tab.
result = project.export.redbrick_format(only_ground_truth=False, task_id="TODO")
```

#### Export in COCO format

```python
# Export data in Coco format
result = project.export.coco_format(only_ground_truth=False)
```

{% hint style="info" %}
COCO format is only supported for the following task types:&#x20;

image bounding box, image polygon, image segmentation.
{% endhint %}

#### Export segmentation labels in PNG format

```python
# Exports PNG masks to local directory named project_id
project.export.redbrick_png(only_ground_truth=False)
```

{% hint style="info" %}
PNG format is only supported for image segmentation projects.
{% endhint %}
