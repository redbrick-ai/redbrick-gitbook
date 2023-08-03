# Exporting Annotations

You can make use of RedBrick AI's Python SDK to export your annotations using a Python script.&#x20;

Within the Python SDK, annotations are exported in two ways:&#x20;

1. The `export_tasks` function **returns a Python object** containing meta-data information and any vector annotations (measurements, landmarks, etc.). Please see the [format of the object here](https://docs.redbrickai.com/python-sdk/reference/export-annotation-format).&#x20;
2. Segmentation data is written to your disk **in NIfTI format**. Segmentation data can also be exported in PNG by manipulating the parameters of the `export_tasks` function. Please view the detailed [`export_tasks` reference here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.export\_tasks).&#x20;

{% hint style="info" %}
If you're attempting a one-time export or don't have intensive requirements for your export, the [**CLI** ](https://docs.redbrickai.com/python-sdk/cli-overview/exporting-annotations)also provides a simple and optimized workflow for exporting a Project's annotations.&#x20;
{% endhint %}

### Code Examples

As always, you should first perform the [standard RedBrick AI SDK setup](./#initializing-the-redbrick-sdk-in-python) to create a Project object.

```python
project = redbrick.get_project(org_id, project_id, api_key)
```

With a new Project object created, you can export your Project's Tasks in various ways. Please see some common examples below.

#### Export All Tasks

```python
annotations = project.export.export_tasks()
```

#### Export Only Ground Truth

You can export only the Tasks in Ground Truth, i.e., Tasks that have successfully made it through all Label and Review Stages.&#x20;

```python
gt_annotations = project.export.export_tasks(only_ground_truth=True)
```

#### **Export Specific Tasks**

Export selected Tasks by specifying Task IDs.&#x20;

```python
specific_annotations = project.export.export_tasks(task_id="...")
```

## Generate an Audit Trail

An audit trail can be useful for regulators interested in your quality control processes, as well as for managing your internal QA processes.&#x20;

{% hint style="success" %}
Please see a detailed reference for[`get_task_events` here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.get\_task\_events).
{% endhint %}

First, perform the [standard RedBrick AI SDK setup](./#initializing-the-redbrick-sdk-in-python) to create a Project object.&#x20;

#### Audit Trail - Ground Truth Tasks Only

Next, retrieve an audit trail for all Ground Truth Tasks**.** Please note that by default, `get_task_events` only returns audit information for Tasks in the Ground Truth Stage.&#x20;

```python
project = redbrick.get_project(org_id, project_id, api_key)

# Return an audit trail for all Tasks currently in the Ground Truth Stage
audit_trail = project.export.get_task_events()
```

#### Audit Trail - All Tasks

If you'd like to generate an audit trail for **all Tasks** (not only those in the Ground Truth Stage), be sure to include the `only_ground_truth=False` parameter.

```python
# Return an audit trail for all Tasks in all Stages
audit_trail = project.export.get_task_events(only_ground_truth=False)
```

The returned object will contain data similar to the code snippet below, where each entry will represent a single Task (uniquely identified by `taskId`). The `events` array contains all key events/actions performed on the Task, with `events[0]` being the first event.

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

### Additional Capabilities

The following is a non-exhaustive list of other available functionalities when using the [`Export` class](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#export). A full list of the capabilities of our `Export` class can be found [here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export).

* Track labeler or reviewer time spent on a Task with [`get_active_time()`](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.get\_active\_time);
* Fetch Task events from a specific timestamp to the present day using [`get_task_events()`](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.get\_task\_events) and the `from_timestamp` parameter;
* Easily search for Tasks based on a wide variety of criteria using [`list_tasks()`](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.list\_tasks);
