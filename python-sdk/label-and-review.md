---
description: >-
  The Label and Review SDK modules allow you to programmatically perform
  labeling and review actions using the redbrick-sdk.
---

# Label and Review

## SDK Review

SDK review works similarly to how you handle review through the UI, you first fetch tasks and their labels, and then you respond with a boolean for each task to determine whether it passes or fails.

### Getting Review Tasks

Retrieve review tasks from your project pipeline. 

```python
tasks = project.review.get_tasks(stage_name, count=1)
```

**`stage_name`**  
You can find the name of your Review stage on the Project overview dashboard. The default names are something like Review\_1.

**`count`**  
Number of review tasks to retrieve, must be an integer between 1 and 50. 

**`tasks`** _returned value_  
****Please see the `TaskObject` format in the [reference documentation.](reference.md)

```javascript
[TaskObject]
```

### Submitting Review Tasks

Submit the review tasks that you had retrieved, and provide a review resolution.

```python
failed = project.review.put_tasks(stage_name, tasks_reviewed)
```

**`stage_name`**  
Same as `stage_name` defined above. 

**`tasks_reviewed`**  
To accept a review task set `reviewVal` to `True.`

```javascript
[
    {
        "taskId": "<unique task id>", // same as the ID retrieved from get_tasks() method
        "reviewVal": bool
    }
]
```

### Code Example SDK Review

```python
import redbrick

api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
stage_name = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)

tasks = project.review.get_tasks(stage_name, count=1)

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

## SDK Label

This works very similar to review except that instead of adding a boolean "reviewVal" for each task, you can add, update, or remove labels. 

### Getting Labeling Tasks

Retrieve labeling tasks from your project pipeline.

```python
tasks = project.labeling.get_tasks(stage_name, count=1)
```

**`stage_name`**  
Name of the manual labeling stage can be found on the Project Overview dashboard. 

**`count`**  
Number of labeling tasks to retrieve, between 1 and 50. 

**`tasks`** _returned value_  
****Please see the `TaskObject` format in the [reference documentation.](reference.md)

```javascript
[TaskObject]
```

### Submitting Labeling Tasks

Submit labeling tasks with labels that you have added. 

```python
failed = project.label.put_tasks(stage_name, tasks_labeled)
```

**`stage_name`**   
Same as stage\_name above. 

**`tasks_labeled`**   
Please see `LabelObject` format in the [reference documentation.](reference.md)

```python
[
    {
        "taskId": "<unique task id>",
        "labels": [LabelObject]
    }
]
```

### Code Example SDK Labeling

```python
import redbrick

api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
stage_name = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)

tasks = project.label.get_tasks(stage_name, count=1)

# Replace with your own logic for labeling tasks
tasks_labeled = [{"taskId": task["taskId"], "labels": task["labels"]} for task in tasks]

failed = project.labeling.put_tasks(stage_name, tasks_labeled)

for failed_task in failed:
    print(
        "failed to update task {} because of {}".format(
            failed_task["taskId"], failed_task["error"]
        )
    )
```

