# Assigning & querying tasks

The SDK offers multiple ways to query/search through your project tasks and programmatically assign them to various users.&#x20;

## Search by task name

Use `search_tasks` to search for tasks by `name` and get their corresponding `task_id`. Often, users will have task `name`s readily accessible, and can use `search_tasks` to get the corresponding `task_id` which may be needed in other SDK functions.&#x20;

{% hint style="success" %}
Please see a detailed reference for [search\_tasks here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.search\_tasks).
{% endhint %}

```python
project = redbrick.get_project(org_id, project_id, api_key)

tasks = project.search_tasks() # fetches all tasks
specific_task = project.search_tasks(name="...") # fetches specific task by name
```

## Assign tasks to a user

Use `assign_task` when you already have the `task_id` you want to assign to a particular user. If you don’t have the `task_id`, you can query all the tasks using [`export_tasks`](exporting-tasks.md#export-all-tasks) or query tasks assigned to a particular user/unassigned tasks using [`get_task_queue`](assigning-and-querying-tasks.md#retrieve-queued-tasks).

{% hint style="success" %}
Please see a detailed reference for [assign\_tasks here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.labeling.Labeling.assign\_tasks).
{% endhint %}

#### Assign to a specific user

```python
project = redbrick.get_project(org_id, project_id, api_key)

# Assign tasks in Label stage to a specific user
project.labeling.assign_tasks(task_id="...", email="...")

# Assign tasks in Review stage to specific user
project.review.assign_tasks(task_id="...", email="...")
```

#### Assign tasks to the current user

You can assign tasks to your API key in the following way:&#x20;

```python
project.labeling.assign_tasks(task_ids=["..."], current_user=True) 
```

## Retrieve queued tasks

Use `get_task_queue` when you want to retrieve the tasks assigned to a particular user, or you want to fetch all the unassigned tasks in your project. This can be useful in preparation for using [`assign_tasks`](assigning-and-querying-tasks.md#assign-tasks-to-a-user) to programmatically assigning unassigned tasks, or [`put_tasks`](programmatic-label-and-review.md) to programmatically label/review tasks assigned to you.

{% hint style="success" %}
Please see a detailed reference for [get\_task\_queue here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.labeling.Labeling.get\_task\_queue).
{% endhint %}

#### Retrieve tasks assigned to specific user

```python
project = redbrick.get_project(org_id, project_id, api_key)

# Get tasks assigned to email@email.com in Label labeling stage
project.labeling.get_task_queue(stage_name="Label", email="email@email.com")

# Get tasks assigned to email@email.com in Review_1 review stage
project.review.get_task_queue(stage_name="Review_1", email="email@email.com")
```

#### Retrieve unassigned tasks

You can also fetch all unassigned tasks in a particular stage along with the ones that are assigned to the current API Key. This information may be useful when choosing which tasks to assign to users.&#x20;

```python
project = redbrick.get_project(org_id, project_id, api_key)

# Get unassigned tasks in Label labeling stage
project.labeling.get_task_queue(stage_name="Label", fetch_unassigned=True)

# Get unassigned tasks in Review_1 review stage
project.review.get_task_queue(stage_name="Review_1", fetch_unassigned=True)
```

## Retrieve tasks assigned to you

Use `get_tasks` to fetch all tasks _already assigned to the current API Key_. This can be useful when re-assigning those tasks to another user (through [`assign_tasks`](assigning-and-querying-tasks.md#assign-tasks-to-a-user)) or for programmatically submitting them through [`put_tasks`](programmatic-label-and-review.md).&#x20;

{% hint style="success" %}
Please see a detailed description of [get\_tasks here](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.labeling.Labeling.get\_tasks).
{% endhint %}

{% hint style="info" %}
Calling this function will **automatically assign** available tasks to your API key as per our [automatic task assignment](../../projects/how-task-assignment-works.md#automatic-task-assignment).\
\
If you want to retrieve tasks assigned to you _without automatically assigning new tasks,_ run `get_task_queue(stage_name="...").`
{% endhint %}

```python
project = redbrick.get_project(org_id, project_id, api_key)

# Get tasks assigned to your API key in Label stage
label_tasks = project.labeling.get_tasks(stage_name="Label")

# Get tasks assigned to your API key in Review_1 stage
review_tasks = project.review.get_tasks(stage_name="Review_1")
```
