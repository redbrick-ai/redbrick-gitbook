# Label and Review

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
Please see the format of [TaskObject in the reference documentation.](../reference/#task-objects)
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
Please see the format of [TaskObject in the reference documentation.](../reference/#task-objects)
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



## Assign tasks to labelers or reviewers

{% hint style="info" %}
You can only assign tasks that are in a given label or review stage. This means you cannot determine the reviewer before a task has been labeled.&#x20;
{% endhint %}

A common thing you might want to do is assign unassigned tasks evenly amongst labelers.

```python
stage_name = "Label" # change to "Review_1"
# After loading sdk project object:
tasks = project.labeling.get_task_queue(stage_name)

assigned = [task for task in tasks if task["assignedTo"]]
unassigned = [task for task in tasks if task["assignedTo"] is None]

labelers = [
    "user1@company.com",
    "user2@company.com",
    "user3@company.com",
    "user4@company.com"
]

# split unassigned tasks evenly amongst labelers
while unassigned:
    for email in labelers:
        
        task = unassigned.pop()
        project.labeling.assign_task(stage_name, task["taskId"], email)
        print(f"Assigned {email} to {task['taskId']}")

        if not unassigned:
            break
```

This same code example can be used to assign reviewers by changing the `stage_name` value to `"Review_2"` or whatever name the stages in your project has.\
``
