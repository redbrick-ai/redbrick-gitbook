# Exporting tasks

## Exporting Annotations

You can use the SDK to export your annotations using a Python script. The CLI also provides a simple and optimized workflow for exporting annotations.&#x20;

Annotations are exported in two ways:&#x20;

1. The `export_tasks` function **returns a Python object** containing important meta-data information and any vector annotations (measurements, landmarks, etc.). Please see the [format of the object here](../reference/).&#x20;
2. Segmentation data is written to your disk in the NIfTI format. Segmentation data can also be exported in PNG format. Please see the [folder structure here](../reference/).&#x20;

{% hint style="success" %}
Please view the detailed [`export_tasks` reference here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.export\_tasks).&#x20;
{% endhint %}

### Code Examples

Perform the [standard RedBrick AI SDK set-up](./#initializing-the-redbrick-sdk-in-python) to create a project object.

```python
project = redbrick.get_project(org_id, project_id, api_key)
```

#### Export all tasks

```python
annotations = project.export.export_tasks()
```

#### Export only ground truth

You can export only the tasks in Ground Truth, i.e., tasks that have successfully made it through all Labeling and Review stages.&#x20;

```python
annotations = project.export.export_tasks(only_ground_truth=True)
```

#### **Export specific tasks only**

Export select tasks by specifying Task IDs.&#x20;

```python
annotations = project.export.export_tasks(task_id=["...", "..."])
```

## Generate an audit trail

Generating an audit trail can be useful material for regulators interested in your quality control processes and for managing your internal QA processes.&#x20;

You can generate a detailed audit trail of all actions/events associated with every task using `get_task_events`.

{% hint style="success" %}
Please see a detailed reference for [`get_task_events` here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.get\_task\_events).
{% endhint %}

Perform the [standard RedBrick AI SDK set-up](./#initializing-the-redbrick-sdk-in-python) to create a project object and retrieve the audit trail for all tasks.

```python
project = redbrick.get_project(org_id, project_id, api_key)
audit_trail = project.get_task_events()
```

Generate the audit trail for all tasks (not only the ones in ground truth).

```python
audit_trail = project.get_task_events(only_ground_truth=False)
```

The returned object will contain data similar to what is shown below. Each entry will represent a single task (uniquely identified by `taskId`). The `events` array contains all key events/actions performed on the task, with `events[0]` being the first event.

```json
[
  {
    "taskId": "...",
    "currentStageName": "Label",
    "events": [
      {
        "eventType": "TASK_CREATED",
        "createdAt": "...",
        "isGroundTruth": false,
        "createdBy": "..."
      },
      {
        "eventType": "TASK_ASSIGNED",
        "createdAt": "...",
        "assignee": "...",
        "stage": "Label"
      }
    ]
  }
]
```
