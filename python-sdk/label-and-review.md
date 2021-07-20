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



