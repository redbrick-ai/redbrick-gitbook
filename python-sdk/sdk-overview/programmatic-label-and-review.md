# Programmatic Label & Review

It may be useful to programmatically add labels to your uploaded data or perform a review on queued tasks. This scenario may arise if you have an automated way of reviewing data or if you want to bulk-process tasks.&#x20;

{% hint style="success" %}
Please see the detailed reference documentation for [`put_tasks` here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.labeling.Labeling.put\_tasks).
{% endhint %}

{% hint style="warning" %}
You can use `put_tasks` only on tasks **assigned to your API key.**

Visit our documentation on assigning tasks to learn how to assign tasks to your API key.
{% endhint %}

First, perform the [standard RedBrick AI SDK set-up](./#initializing-the-redbrick-sdk-in-python) to create a project object.

```
project = redbrick.get_project(org_id, project_id, api_key)
```

Next, you need to get a list of tasks you want to label/review. You can do this by:&#x20;

1. Searching for the `task_id` through the RedBrick AI UI.
2. Retrieving the `task_id` from your filename/custom `name` from the Items List, using [search\_tasks](exporting-tasks.md#query-tasks-in-your-project).
3. Retrieving tasks assigned to your API key using `get_tasks`.

#### Programmatically label tasks

Add your annotations within the `labels` field, along with the `task_id`. The corresponding task must be queued in the Label stage and assigned to your API key.&#x20;

```python
tasks = [
    {
        "task_id": "...",
        "labels": [{...}]
    },
]

# Unless you renamed your label stage, it would be called "Label". 
# You can find the name on the Overview dashboard workflow chart. 
project.labeling.put_tasks(stage_name="Label", tasks=tasks)
```

#### Programmatically review tasks

Add your review decision in the `reviewVal` field, along with the `task_id`. The corresponding task must be queued in the Review stage that you specify in `stage_name` and must be assigned to your API key.

```python
tasks = [
    {
        "task_id": "...",

        # Set reviewVal to True if you want to accept the task
        "reviewVal": True
    },
    {
        "task_id": "...",

        # Set reviewVal to False if you want to reject the task
        "reviewVal": False
    }
]

# Unless you re-named your Review stages, they will be Review_1, Review_2...
project.review.put_tasks(stage_name="Review_1", tasks=tasks)
```

## Re-annotate Ground Truth Tasks

Once your task goes through all workflow stages, it will be stored in the Ground Truth stage. If you notice issues with one or more of your Ground Truth tasks, you can either directly correct them in the Ground Truth stage through the UI or **send them back to the Label** stage for correction.

First, get a list of the `task_id`s you want to send back to Label. You can do this by [exporting only ground truth tasks](exporting-tasks.md#export-only-ground-truth) and filtering them. Then, use `move_tasks_to_start` to send them back to Label.

```python
task_ids = ["...", "..."]
project.labeling.move_tasks_to_start(task_ids=task_ids)
```

{% hint style="warning" %}
All corresponding Tasks need to be in the Ground Truth stage. This function will not work for tasks queued in Review.&#x20;
{% endhint %}
