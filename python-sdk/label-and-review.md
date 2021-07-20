---
description: Automatically handle label or review tasks using the RedBrick SDK.
---

# Label and Review

### SDK Review

SDK review works similarly to how you handle review through the UI, you first fetch tasks and their labels, and then you respond with a boolean for each task to determine whether it passes or fails.

To pass a task, set "reviewVal" to True. 

To fail a task, set "reviewVal" to False.

```python
import redbrick

api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
stage_name = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)

tasks = project.review.get_tasks(stage_name, num_tasks=1)

# Replace with your own logic for reviewing tasks
tasks_reviewed = [{"taskId": task["taskId"], "reviewVal": True} for task in tasks]

failed = project.review.put_tasks(stage_name, tasks_reviewed)

for failed_task in failed:
    print(
        "failed to update task {} because of {}".format(
            failed_task["taskId"], failed_task["error"]
        )
    )

```

The format of the task objects looks like: 

```python
{
     "taskId": "<unique task id>",
     "labels": [LabelObject],  
     "items": [str], # Unsigned URL's 
     "itemsPresigned": [str],  # URL's to download images
     "name": str  # unique name given when creating a datapoint
}
```

And the format of the object that you upload to `project.review.put_tasks`

```python
{
    "taskId": "<unique task id>",
    "reviewVal": bool
}
```

### SDK Label

This works very similar to review except that instead of adding a boolean "reviewVal" for each task, you can add, update, or remove labels. The example below should work to get you started on any project.



```python
import redbrick

api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
stage_name = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)

tasks = project.label.get_tasks(stage_name, num_tasks=1)

# Replace with your own logic for labeling tasks
tasks_labeled = [{"taskId": task["taskId"], "labels": task["labels"]} for task in tasks]

failed = project.label.put_tasks(stage_name, tasks_labeled)

for failed_task in failed:
    print(
        "failed to update task {} because of {}".format(
            failed_task["taskId"], failed_task["error"]
        )
    )
```

The format of the task objects is the same as when reviewing tasks \(see above\).

The format of the object you upload to submit a task looks like

```python
{
    "taskId": "<unique task id>",
    "labels": [LabelObject]
}
```

 



