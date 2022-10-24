# How task assignment works

## What is a task?

A task is either a single image, series, or entire study that moves through the annotation workflow in a single unit. The intention is for a labeler to view and annotate a single task together; therefore, if you'd like your annotators to view & annotate an entire MRI study comprised of 4 series together, you should upload the entire study as a single task.

Please read the [data import documentation](../importing-data/import-cloud-data.md#items-list) to understand how to import data as a single image/series/entire study task.

## Task Assignment&#x20;

Task assignment helps manage the delegation of work amongst your entire team. RedBrick AI has automatic task assignment protocols, but you can override these with manual/programmatic task assignment as well.

{% hint style="warning" %}
Labelers can only view tasks that are assigned to them. Admins can view all tasks, but only modify tasks that are assigned to them.&#x20;
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

[Please visit our SDK documentation](../python-sdk/sdk-overview/label-and-review.md#assign-tasks-to-labelers-or-reviewers) for an overview of programmatically assigning tasks.&#x20;

{% embed url="https://www.loom.com/share/2c71c7fd4f0c49ef8d34f2b9847b30c0" %}
