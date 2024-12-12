# Consensus

Consensus provides you with both a quantitative measure of annotation quality (by means of an Inter-Annotator Agreement Score) and the opportunity to create higher-quality annotations by combining the opinions of multiple annotators.&#x20;

## How Does Consensus Work?&#x20;

With Consensus enabled, **multiple annotators can be required to label each Task** in the Label Stage. Each individual annotator will only see an empty Task and will not be able to view the annotations done by the other annotators.

<figure><img src="../../../.gitbook/assets/image (24).png" alt="" width="563"><figcaption><p>Comparison between standard flow and Consensus flow with 3 labelers</p></figcaption></figure>

Once all the annotators have completed the Task, RedBrick AI will calculate an **Inter-Annotator Agreement Score** between the annotations. Please reference the [following documentation](./#inter-annotator-agreement) for more information on how we calculate these scores.

The Inter-Annotator Agreement Score is a quantitative measure of quality that can help you select the best set of annotations created by your annotators. It also gives reviewers the ability to arbitrate between the opinions of multiple annotators before generating a single, high-quality Ground Truth.&#x20;

## Enabling Consensus

As of v1.1.2, you must enable Multiple Labeling for your Project upon Project creation.

Once enabled, complete step (4) of Project creation by selecting a **minimum number of labelers** that will be required to annotate each Task. If your project has a Review Stage, you can **enable auto-acceptance** to automatically accept Tasks whose agreement scores are higher than the specified threshold.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-08-30 at 11.15.34@2x.png" alt=""><figcaption></figcaption></figure>

## Assigning Tasks to Multiple Users

RedBrick AI has an [**Automatic Assignment Protocol**](../../../projects/tasks-and-assignment.md#automatic-task-assignment) that will automatically assign multiple users to a Task. This protocol is enabled by default on Project creation and can be configured either when creating your Project or any time afterward in your Project's [General Settings](../../settings-page/#general-settings).

As annotators request Tasks by clicking on the **Label** button in the top right of the Dashboard, RedBrick AI will automatically assign available Tasks by prioritizing those that are already in progress/or assigned to other users. &#x20;

Alternatively, you can **manually override any Task assignment on the Data page**. When Consensus is enabled, the **Assign** dropdown will allow you to select multiple users.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-08-30 at 11.17.46@2x.png" alt=""><figcaption><p>Task assignment in a Consensus Project</p></figcaption></figure>

{% hint style="info" %}
Optionally, you can manually assign any number of labelers to a Consensus Task, including a number that is greater than the minimum number of required labelers. However, the Automatic Assignment Protocol will only assign up to the minimum value.&#x20;
{% endhint %}

## Inter-Annotator Agreement

Once all assigned annotators have completed a Task, RedBrick AI will generate an Inter-Annotator Agreement Score, which is calculated by comparing each labeler's annotations with those of every other labeler and averaging the pairs of scores.

<table><thead><tr><th> </th><th width="157">User 1</th><th>User 2</th><th width="250">User 3</th></tr></thead><tbody><tr><td>User 1</td><td></td><td><mark style="color:blue;"><code>Score(U1,U2)</code></mark></td><td><mark style="color:purple;"><code>Score(U1,U3)</code></mark></td></tr><tr><td>User 2</td><td><mark style="color:blue;"><code>Score(U2,U1)</code></mark></td><td></td><td><mark style="color:orange;"><code>Score(U2,U3)</code></mark></td></tr><tr><td>User 3</td><td><mark style="color:purple;"><code>Score(U3,U1)</code></mark></td><td><mark style="color:orange;"><code>Score(U3,U2)</code></mark></td><td></td></tr></tbody></table>

`Agreement = Average(`<mark style="color:blue;">`Score(U1,U2)`</mark>`,`<mark style="color:purple;">`Score(U1,U3)`</mark>`,`<mark style="color:orange;">`Score(U2,U3)`</mark>`).`

The type of comparison function used to calculate the `Score`depends on the type of data and annotations you and your team are working with. Please reference the following documentation to read more about how RedBrick calculates Inter-Annotator Agreement.

{% content-ref url="agreement-calculation.md" %}
[agreement-calculation.md](agreement-calculation.md)
{% endcontent-ref %}

![Inter-Annotator Agreement for Tasks queued in Review](<../../../.gitbook/assets/Screen Shot 2022-08-16 at 12.27.55 PM.png>)

## Review Stage Absent

If there is no Review Stage after the Label Stage, the set of annotations with the highest Agreement Score (with respect to other annotations) will be selected and stored in Ground Truth. This is the set of annotations that will be exported by default, but you can also export all versions of the annotations.&#x20;

## Review Stage Present

When a Review Stage is present, the annotation sets of all labelers will be displayed in the Annotation Tool.&#x20;

The users that annotated the Task will be listed in the lefthand toolbar. By default, annotations are color-coded **by user**, but the Consensus Reviewer can also control the visibility of each Object Label Entity individually.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-08-30 at 11.25.05@2x.png" alt=""><figcaption></figcaption></figure>

## Best Annotations and Super Truth

The reviewer’s primary task is to analyze the multiple sets of annotations generated by the labelers and produce a single set that will be saved and pushed to the next Stage. In RedBrick AI's Editor, this single set of annotations is referred to as the **Best Annotations**.

{% hint style="info" %}
By default, RedBrick AI selects the set of annotations with the highest Inter-Annotator Score as the Best Annotations.
{% endhint %}

Reviewers can view, hide/show, etc. all sets of annotations in a Task. This allows the reviewer to analyze the work done by the labelers and select the set of annotations that they consider to be of the highest quality.

If a reviewer is satisfied with an existing annotation set, they can simply designate it as Best Annotations and accept the Task.

If a reviewer wishes to make changes to an existing set of annotations or start completely from scratch, they can either click on the **Edit** button under a user in the right hand panel or click on **Create New** under Super Truth.&#x20;

Doing so will create a novel set of annotations known as a **Super Truth** and automatically designate the set as Best. The reviewer can then annotate the Task as they see fit.

{% hint style="warning" %}
**Only Super Truth Annotations can be edited!**&#x20;

All other annotations in the Review Stage are View Only.
{% endhint %}

Once a reviewer is satisfied with the current Best Annotations, they can accept the Task. This saves the Best Annotations and ascribes only that set to the Task. All other annotations are also saved and are available on export. If the reviewer rejects the Task, **all labelers will be required to re-annotate the task**.

The video below contains a brief walkthrough of how you can use Consensus in both your Project and the Editor.&#x20;

{% embed url="https://www.loom.com/share/62f152ff8b924d61abe6d8ea31672c22" %}

## Exporting Consensus Annotations

If a task has gone through Consensus, you will get access to all versions of the annotations done by all users. You will also have access to additional metadata like the annotation similarity scores. You can export the data using the following CLI command inside your project directory:

```bash
redbrick export 
```

Please [view the format reference](../../../python-sdk/formats/full-format-reference.md#consensus-export) for an overview of the exported format.

If you want to export only a single version of the annotations (i.e. the labeler with the best annotations or the base annotations qualified in Review), you can run the following command:

```bash
redbrick export --no-consensus
```
