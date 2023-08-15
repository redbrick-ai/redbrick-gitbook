# Task Assignment

## What is a Task?

A Task is either a single image, series, or entire study that moves through the annotation workflow in a single unit. The intention is for a Labeler to view and annotate a single Task together; therefore, if you'd like your Labelers to view & annotate an entire MRI study comprised of 4 series together, you should upload the entire study as a single Task.

Please read the [data import documentation](../importing-data/import-cloud-data.md#items-list) to understand how to import data as a single image/series/entire study.

## Overview&#x20;

Task assignment helps manage the delegation of work amongst your entire team. RedBrick AI has automatic task assignment protocols, but you can override these with manual/programmatic task assignment as well.

{% hint style="warning" %}
Labelers (i.e. Project Members) can only view Tasks that have been assigned to them. Admins can view all Tasks but only modify tasks assigned to them.&#x20;
{% endhint %}

### **Automatic Task Assignment**

All projects use automatic task assignment by default. The automatic task assignment protocol is a first-come-first-serve system that assigns the _oldest_ data to the annotators that request new tasks first.

Labelers can request new tasks by keeping the Annotation Tool open or clicking on the "Label/Review" buttons on the Project Dashboard.

{% hint style="info" %}
You can disable automatic task assignment in **Project Settings -> Overview.**
{% endhint %}

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_team (5).png" alt=""><figcaption></figcaption></figure>

### **Manual Assignment**

You can override the automatic assignment protocol by manually assigning tasks to users from the Data Page.&#x20;

{% hint style="info" %}
RedBrick AI will not automatically re-assign tasks that you have manually assigned.&#x20;
{% endhint %}

### **Programmatically Assigning Tasks**

You can programmatically assign tasks using our SDK or prescribe the assignment during data upload as part of your [items file](../importing-data/import-cloud-data/creating-an-items-list.md#upload-an-items-list-to-your-project).

#### Prescribe Assignment on Upload

You can use the [`preAssign`](../python-sdk/format-reference.md#preassign-stagename-string-string) field in the items file to assign a Task to a specific user(s) at each Stage.

For example, the snippet below will assign `study01` to `annotator@email.com` in the Label Stage. Once the annotation is complete, the Task will be queued in `Review_1` and `reviewer@email.com` will be assigned as the Reviewer.

{% hint style="info" %}
Always double check that your Stage Names (i.e., Label, Review\_1, etc.) and user emails have been input correctly.&#x20;

Also, when preassigning Tasks, all emails must be associated with an existing Project Member.
{% endhint %}

```json
[
    {
        "name": "study01", 
        "preAssign": {
            "Label": "annotator@email.com",
            "Review_1": "reviewer@email.com"
        },
        "series": [
            {
                "items": "file.nii.gz", 
            }
        ]
    }
]
```

#### Assign Tasks using the SDK

Please visit our [SDK documentation](https://docs.redbrickai.com/python-sdk/sdk-overview/assigning-and-querying-tasks) for an overview of how to assign Tasks programmatically.&#x20;

{% embed url="https://www.loom.com/share/2c71c7fd4f0c49ef8d34f2b9847b30c0" %}

## Labeling Queue

Once a task is assigned to a user, it is added to their Labeling Queue. You can view your labeling queue in two ways.

1. **From the Data Page:** \
   [On the Data Page](https://app.tango.us/app/workflow/Labeling-Queue-on-Data-Dashboard-b79b4d8562d34bc6a33d6cce0aa4476e), you can filter existing Tasks by **Queued for Labeling/Review** and then by Tasks assigned to you.
2. **In the Annotation Tool:**\
   [The Labeling Queue](https://app.tango.us/app/workflow/View-Labeling-Queue-in-Tool-17a013c7a161415c85cba3369344cae2) can be expanded/retracted by clicking on the corresponding button in the top bar of the Annotation Tool.&#x20;

While in your Queue, a Task can be in a few different states depending on the status of the annotation:&#x20;

1. **Assigned**\
   Tasks that you have not worked on yet will be displayed as Assigned.
2. **Saved**\
   Once you save your in-progress annotation (either manually or through auto-save), the Task will show as saved.&#x20;
3. **Pending Finalization**\
   Once you are done with the annotation, you can **Submit a Draft**. All drafts that have been submitted will **still be in your Labeling Queue** pending finalization. You must finalize the draft to complete it and send it to the next stage of the workflow.
4. **Skipped**\
   If you encounter a Task that you would like to complete at a later time, you can skip it to send it to the end of your Labeling Queue.&#x20;

The diagram below is a visual guide to the flows associated with completing Tasks in your Labeling Queue, including associated actions and Task states.

<figure><img src="../.gitbook/assets/Group 30489 (3).png" alt=""><figcaption><p>Guide to submitting Tasks in your Labeling Queue</p></figcaption></figure>

### Task Prioritization

RedBrick AI allows you to designate specific Tasks as **prioritized**, which elevates them to the top of your Labeling Queue.

Task Priority is reflected in the Web Application in the following ways:

1. Task Priority is visible in the Data Page when sorting by **Queued for Labeling/Review** or **Recently Labeled/Reviewed** - this logic applies to all Stages except for Ground Truth.
2. Task Priority will persist throughout Raising an Issue and/or Rejecting a Task at any Stage.
3. Task Priority will be visible in the Annotation Tool when viewing the Queue
4. Tasks that are Assigned and Prioritized will occupy a higher position in the queue than Tasks that are Unassigned and Prioritized.

As seen in the snippet below, you can use the [`update_tasks_priority()`](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#labeling) method to designate a float between 0 and 1 that reflects the priority of a given Task (where 1 is the highest priority and 0 is the lowest).

```python
tasks = 
    [
        {
            # High Priority Task
            "taskId": "2716057",
            "priority": 0.95
        },
        {
            # Mid Priority Task
            "taskId": "BU221729",
            "priority": 0.50
        },
        {
            # Low Priority Task
            "taskId": "8675309",
            "priority": 0.32
        }
]
    
project.labeling.update_tasks_priority(
    stage_name="Label", 
    tasks=tasks
)
```

{% hint style="info" %}
For the truly brave, our Prioritization API supports up to the billionth place for floats.
{% endhint %}
