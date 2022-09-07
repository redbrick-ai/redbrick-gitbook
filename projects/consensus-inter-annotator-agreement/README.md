# Consensus (Inter-annotator Agreement)

Consensus gives you a quantitative measure of the quality of annotations (through an inter-annotator agreement score), and the opportunity to create higher-quality annotations by combining the opinion of multiple annotators.&#x20;

## How does consensus work?&#x20;

When consensus is enabled, **multiple annotators can be required to label each** task in the labeling stage. Each individual annotator will see an empty task, and will not be able to view the annotations done by the other annotators.&#x20;

Once all the annotators have completed the task, RedBrick AI will **calculate an inter-annotator agreement score** between the annotations. Please visit the [following documentation](./#inter-annotator-agreement) to see how we calculate agreement scores.

The inter-annotator agreement score gives you a quantitative measure of quality. This will help you select the best set of annotations created, and/or give reviewers the ability to arbitrate between the opinion of multiple annotators to generate a single source of high-quality ground truth.&#x20;

## Enabling consensus

You can enable consensus in project settings. Once enabled, you will be required to select a **minimum number of labelers** that will be required to annotate each task. If your project has a review stage, you can enable **auto-acceptance** to automatically accept tasks whose agreement scores are higher than the specified threshold.&#x20;

![Consensus project settings](../../.gitbook/assets/localhost\_3000\_943c97cd-58b1-4794-84d0-8b00d26f0c84\_projects\_64e8b5d9-81d3-4401-a49a-924d72916b0f\_settings.png)

## Assigning tasks to multiple users

RedBrick AI has an **automatic assignment protocol** that will automatically assign multiple users per task. As users request for tasks (by clicking on the label button on the top right of the dashboard), RedBrick AI will automatically assign available tasks by prioritizing tasks that already are in progress/or assigned to other users. &#x20;

You have the option to **manually override any task assignment through the data page**. When consensus is enabled, the assign dropdown will allow you to select multiple users.

![Manual multi-assignment](<../../.gitbook/assets/Screen Shot 2022-08-16 at 12.03.37 PM.png>)

{% hint style="info" %}
You can _manually_ assign more than the required number of annotators. The automatic assignment protocol will only assign up to the number of required labelers, but you can manually assign as many as you'd like.&#x20;
{% endhint %}

## Inter-annotator agreement

Once all assigned annotators have completed a task, RedBrick AI will calculate an inter-annotator agreement score. The inter-annotator agreement is calculated by comparing each labeler's annotations with every other labeler, and averaging pairs of scores.

|        | User 1                                            | User 2                                            | User 3                                            |
| ------ | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| User 1 |                                                   | <mark style="color:blue;">`Score(U1,U2)`</mark>   | <mark style="color:purple;">`Score(U1,U3)`</mark> |
| User 2 | <mark style="color:blue;">`Score(U2,U1)`</mark>   |                                                   | <mark style="color:orange;">`Score(U2,U3)`</mark> |
| User 3 | <mark style="color:purple;">`Score(U3,U1)`</mark> | <mark style="color:orange;">`Score(U3,U2)`</mark> |                                                   |

`Agreement = Average(`<mark style="color:blue;">`Score(U1,U2)`</mark>`,`<mark style="color:purple;">`Score(U1,U3)`</mark>`,`<mark style="color:orange;">`Score(U2,U3)`</mark>`).`

Depending on the type of data and annotations, a different comparison function is used to calculate the `Score.` Please visit the following documentation to read how this is done.

{% content-ref url="agreement-calculation.md" %}
[agreement-calculation.md](agreement-calculation.md)
{% endcontent-ref %}

![Inter-annotator agreement for tasks queued in review](<../../.gitbook/assets/Screen Shot 2022-08-16 at 12.27.55 PM.png>)

### No Review Stage

If there is no review stage after the labeling stage, the set of annotations with the highest agreement score with respect to other annotations, will be selected and stored in ground truth. By default, this is the set of annotations that will be exported, but you will have the option of exporting all versions of the annotations.&#x20;

### Review Stage Present

When there is a review stage present, all annotations will be displayed on the interface. You can see the list of all users that have annotated the task on the right side Consensus panel. **** Annotations are color-coded _by user_ but can be changed to grouped _by category._

![](<../../.gitbook/assets/localhost\_3000\_943c97cd-58b1-4794-84d0-8b00d26f0c84\_projects\_64e8b5d9-81d3-4401-a49a-924d72916b0f\_tool\_Review\_1\_taskid=582df520-51e9-4357-b88a-b8d709132bdb (1).png>)

#### Base Annotations

The reviewer needs to arbitrate between the multiple sets of annotations and produce a single set of annotations that will get saved. By default, RedBrick AI selects the best set of annotations as the **base annotation.** Reviewers can view, hide/show, etc. all sets of annotations, but can only edit base annotations. You can change the base annotations on the right side consensus panel, by clicking on the "star" icon next to any user.&#x20;

Once the reviewer is done editing the base annotations, or they are happy with the current state of the base annotations, they can accept the task with this single set of annotations (the other annotations are also saved and available on export). If the reviewer rejects the task, **all annotators will be required to re-annotate the task.**

Watch this video for an overview of reviewing a consensus task:

{% embed url="https://www.loom.com/share/3024eebe360a4715ac86af55e361d64e" %}
Consensus review
{% endembed %}

## Exporting Consensus Annotations

If a task has gone through consensus, you will get access to all versions of the annotations done by all users. You will also have access to additional metadata like the annotation similarity scores. You can export the data using the following CLI command inside your project directory:

```bash
redbrick export 
```

Please [view the format reference](../../python-sdk/reference/annotation-format.md#consensus-export) for an overview of the exported format.

If you wanted to export only a single version of the annotations i.e. the annotator with the best annotations or the base annotations qualified in review, you can run the following command:

```bash
redbrick export --no-consensus
```
