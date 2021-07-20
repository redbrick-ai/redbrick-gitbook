---
description: >-
  This documentation covers the basics of interacting with Active Learning
  through the RedBrick SDK. This is useful to integrate your models and
  processes alongside active learning.
---

# Active Learning

### Getting training data

The first step to utilizing active learning will be to export the labeled and unlabeled data from your project. This is done using the following method

```text
try:
    learning_info = project.learning.get_learning_info()
    
except Exception as error:
    print("No jobs ready")
```

The learning\_info object above has the following fields:

```text
learning_info = {
    "unlabeled": [UnlabeledObject],
    "labeled": [LabeledObject],
    "cycle": int,
    "taxonomy": TaxonomyObject
} 

UnlabeledObject
{
  "taskId": str,
  "dpId"; str,
  "items": [str],
  "itemsPresigned": [str],
  "name"; str
}

LabeledObject
{
  "taskId": str,
  "dpId"; str,
  "items": [str],
  "itemsPresigned": [str],
  "name"; str,
  "labels": [RBLabelObject]
}  
```

The `RBLabelObject` and `TaxonomyObject` can be found in the reference section.

```text
post_learning_tasks = []
for task in learning_info["unlabeled"]:

    task_id = task["taskId"]
    post_learning_tasks.append({"score": 0.5, "labels": [], "taskId": task_id})

project.learning.update_tasks(learning_info["cycle"], post_learning_tasks)
```

