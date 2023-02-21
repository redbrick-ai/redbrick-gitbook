# How task assignment works

## What is a task?

A task is either a single image, series, or entire study that moves through the annotation workflow in a single unit. The intention is for a labeler to view and annotate a single task together; therefore, if you'd like your annotators to view & annotate an entire MRI study comprised of 4 series together, you should upload the entire study as a single task.

Please read the [data import documentation](../importing-data/import-cloud-data/#items-list) to understand how to import data as a single image/series/entire study task.

## Task Assignment&#x20;

Task assignment helps manage the delegation of work amongst your entire team. RedBrick AI has automatic task assignment protocols, but you can override these with manual/programmatic task assignment as well.

{% hint style="warning" %}
Labelers can only view tasks that are assigned to them. Admins can view all tasks but only modify tasks assigned to them.&#x20;
{% endhint %}

### **Automatic Task Assignment**

All projects use automatic task assignment by default. The automatic task assignment protocol is a first-come-first-serve system that assigns the _oldest_ data to the annotators that request new tasks first.

Annotators request for new tasks by keeping the labeling tool open or clicking on Label/Review on the project dashboard. If a user becomes inactive for extended periods of time, their automatically assigned tasks will be assigned to other users who are active.&#x20;

{% hint style="info" %}
You can disable automatic task assignment from **Project Settings -> Overview.**
{% endhint %}

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_team (5).png" alt=""><figcaption></figcaption></figure>

### **Manual Assignment**

You can override the automatic assignment protocol by manually assigning tasks to users from the Data page.&#x20;

{% hint style="info" %}
RedBrick AI will not automatically re-assign tasks that you have manually assigned.&#x20;
{% endhint %}

### **Programmatically assigning tasks**

You can programmatically assign tasks using our SDK or prescribe the assignment during data upload as part of your [items file](../importing-data/import-cloud-data/creating-an-items-list.md#upload-an-items-list-to-your-project).

#### Prescribe assignment on upload

You can use [`preAssign`](../python-sdk/reference/annotation-format.md#preassign-stagename-string-string) the field in the items file to define which user will be assigned the task at each stage. For example, the snippet below will assign `study01` to `annotator@email.com` in the `Label` stage. Once the annotation is complete, and the task is queued in `Review_1`, `reviewer@email.com` will be assigned as the Reviewer.

{% hint style="info" %}
Ensure to correctly input the stage names, i.e., Label, Review\_1, etc. Also, make sure to input the users' emails correctly. They must be a member of the project.
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

#### Assign tasks using the SDK

[Please visit our SDK documentation](broken-reference) for an overview of programmatically assigning tasks.&#x20;

{% embed url="https://www.loom.com/share/2c71c7fd4f0c49ef8d34f2b9847b30c0" %}

## Labeling Queue

Once a task is assigned to a user, it is added to their Labeling Queue. You can view your labeling queue in two ways.

1. **From the data page:** \
   ****[On the data page](https://app.tango.us/app/workflow/Labeling-Queue-on-Data-Dashboard-b79b4d8562d34bc6a33d6cce0aa4476e), you can filter by queued for labeling/review and then filter by tasks assigned to you.
2. **On the Labeling Tool:**\
   ****[The labeling queue](https://app.tango.us/app/workflow/View-Labeling-Queue-in-Tool-17a013c7a161415c85cba3369344cae2) is available on the top bar of the labeling tool.&#x20;

While in your Queue, the task can be in a few different states, depending on the status of the annotation:&#x20;

1. **Assigned**\
   ****Tasks that you have not worked on yet will be displayed as Assigned.
2. **Saved**\
   ****Once you save your in-progress annotation (either manually or through auto-save), the task will show as saved. ****&#x20;
3. **Pending Finalization**\
   ****Once you are done with the annotation, you can _Submit the draft_. All drafts that have been submitted will **still be in your labeling queue** __ pending finalization. You must finalize the draft to complete it and send it to the next stage of the workflow.
4. **Skipped**\
   ****Skipped tasks are intended to come back to in the future. If you encounter a task you don't want to complete, you can skip it, and it will be sent to the end of your labeling queue.&#x20;

The diagram below is a guide to completing tasks in your labeling queue, including the actions and states of tasks.

<figure><img src="../.gitbook/assets/Group 30489 (3).png" alt=""><figcaption><p>Guide to submitting tasks in your labeling queue</p></figcaption></figure>
