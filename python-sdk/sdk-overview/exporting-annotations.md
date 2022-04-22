# Exporting Annotations

Please have a look at the [Reference Format](../reference/) for an overview of the export formats.&#x20;

### Code Example

Perform the standard RedBrick AI SDK set-up to create a RBProject object

```python
import redbrick

# Standard Setup
api_key = "<TODO>"
org_id = "<TODO>"
project_id = "<TODO>"

project = redbrick.get_project(
    org_id=org_id,
    project_id=project_id,
    api_key=api_key
)
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

image bounding box and image polygon
{% endhint %}

#### Export segmentation labels in PNG format

```python
# Exports PNG masks to local directory named project_id
project.export.redbrick_png(only_ground_truth=False)
```

{% hint style="info" %}
PNG format is only supported for image segmentation projects.
{% endhint %}

#### Export segmentation labels in NIfTI format

```python
# Exports PNG masks to local directory named project_id
project.export.redbrick_nifti(only_ground_truth=False)
```

{% hint style="info" %}
PNG format is only supported for DICOM segmentation projects.
{% endhint %}
