# Programmatically Label and Review

You can use the RedBrick AI SDK to programmatically label and review your data. If you have an automated method of generating labels / reviews, or want to update tasks in bulk, this is a good option.&#x20;

## Programmatically Label

Perform the standard SDK set up to create a RBProject object.

```python
import redbrick

api_key = "<TODO>"
org_id = "<TODO>"
project_id = "<TODO>"
stage_name = "<TODO>"

project = redbrick.get_project(
    org_id=org_id,
    project_id=project_id,
    api_key=api_key
)
```

Get tasks from your RedBrick AI project. You can find the `stage_name` on the workflow visualization on the project dashboard.

{% hint style="info" %}
Please see the format of [TaskObject in the reference documentation.](reference.md#task-objects)
{% endhint %}

```python
# We recommend keeping the count < 50
tasks = project.label.get_tasks(stage_name, count=1)
```

Add labels to the task entries in the `tasks` object above.&#x20;

```python
# Replace this code with your method of adding labels and creating
# the tasks_labeled list. 

tasks_labeled = []
for task in tasks:
    tasks_labeled += [
        {
            "taskId": task["taskId"], 
            "labels": task["labels"]
        }
    ]
```

Upload the labeled tasks to RedBrick AI

```python
project.labeling.put_tasks(stage_name, tasks_labeled)
```

## Programmatically Review&#x20;

Get review tasks from the RedBrick Ai platform.&#x20;

{% hint style="info" %}
You can find the `stage_name` from the workflow visualization on the project overview dashboard.
{% endhint %}

```python
# We recommend keeping count < 50
tasks = project.review.get_tasks(stage_name, count=1)
```

{% hint style="info" %}
Please see the format of [TaskObject in the reference documentation.](reference.md#task-objects)
{% endhint %}

Review the tasks programmatically and upload

```python
# Replace with your own logic for reviewing tasks
tasks_reviewed = []
for task in tasks:
    tasks_reviewed += [
        {"taskId": task["taskId"], "reviewVal": True} # reviewVal True accepts the task
                                                      # False will fail.
    ]

project.review.put_tasks(stage_name, tasks_reviewed)
```
