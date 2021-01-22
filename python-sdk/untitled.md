# Remote Labeling

The remote labeling module of the SDK provides an interface to interact with your remote labeling stage in your project pipeline. The remote labeling stage is used to import predictions from a model, algorithm, or any other method. The remote labeling module has been designed with flexibility in mind, giving users control over how they are generating, and importing predictions.

## Overview

```python
redbrick.remote_label.RemoteLabel(org_id: str, project_id: str, stage_name: str)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Description |
| :--- | :--- |
| `org_id` | Your organization id, can be found in the url `https://app.redbrickai.com/<org_id>/` |
| `project_id` | The id of the project with the remote-labeling stage. Can be found in the url of the project dashboard `https://app.redbrickai.com/<org_id>/projects/<project_id>` |
| `stage_name` | The name of the `remote-labeling` stage |
{% endtab %}

{% tab title="Methods" %}
| Method | Description |
| :--- | :--- |
| `get_task(num_tasks: int)` | Get's the next task\(s\) from the pipeline. Returns list of [`Task`](https://docs.redbrickai.com/sdk/entities/task/) objects. |
| `submit_task(task: Task, label: label)` | Submits the task with the labels for that task. Requires the [`Task`](https://docs.redbrickai.com/sdk/entities/task/) object from `get_task` and label is one of the label object types - [ImageBoundingBox](https://docs.redbrickai.com/sdk/entity/labels/boundingbox/), [VideoBoundingBox](https://docs.redbrickai.com/sdk/entity/labels/boundingbox/), [VideoClassification](https://docs.redbrickai.com/sdk/entity/labels/classify/) etc. |
| `get_num_tasks()` | Returns the number of tasks queued in this stage |
{% endtab %}
{% endtabs %}

## Usage

**Initializing the module**

You first have to initialize the module by providing all the relevant organization and project details

```python
import redbrick

# Initialize sdk and remote-labeling module
redbrick.init(api_key="<key>")
remote_labeling = redbrick.remote_labeling.RemoteLabel(
    org_id="<org_id>", project_id="<project_id>", stage_name="<stage_name>"
)
```

**Retrieving tasks**

Each datapoint is converted into a task inside a pipeline. The first step in adding model/algorithm generated pre-labels to your tasks, is to retrieve the tasks from the backend.

```python
# Get task from remote
tasks = remote_labeling.get_task(num_tasks=1)
```

The `tasks` variable here is a list of [`Task`](https://docs.redbrickai.com/sdk/entity/task) objects.

**Submitting tasks**

Now that you have the task, you can generate your labels using a model, algorithm or rule based system. You have to submit these labels to the backend in the following manner.

```python
from redbrick.entity.label.bbox import ImageBoundingBox

# Submit task to remote
image_bbox = ImageBoundingBox(labels) # labels is a variable of the correct format
remote_labeling.submit_task(task=tasks[0], labels=image_bbox)
```

