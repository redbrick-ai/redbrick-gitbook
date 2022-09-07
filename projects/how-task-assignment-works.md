# How task assignment works

Task assignment helps manage labeling and review and delegation of work amongst your entire team. RedBrick AI has automatic task assignment protocols, but you can override these with manual/programmatic task assignment as well. This section of the documentation will cover all the details of task assignment.&#x20;

* **Automatic Assignment.** When Labelers/Admins click on the Label/Review button on the top right of the dashboard, RedBrick will automatically assign them tasks in batches of 5. As users keep completing tasks, RedBrick will search the available tasks and assign them additional tasks to work on. \
  \
  If a user becomes inactive for extended periods of time, their automatically assigned tasks will be come available once again, and will be assigned to other users who are active.&#x20;
* **Manual Assignment.** You can override the automatic assignment protocol by manually assigning tasks to users from the Data page. RedBrick AI will not automatically re-assign tasks that you have manually assigned.&#x20;
* **Programmatically assigning tasks.** [Please visit our SDK documentation](../python-sdk/sdk-overview/label-and-review.md#assign-tasks-to-labelers-or-reviewers) for an overview of programmatically assigning tasks.&#x20;

{% hint style="warning" %}
Labelers can only view tasks that are assigned to them. \
Admins can view all tasks, but only modify tasks that are assigned to them.&#x20;
{% endhint %}

{% embed url="https://www.loom.com/share/2c71c7fd4f0c49ef8d34f2b9847b30c0" %}
