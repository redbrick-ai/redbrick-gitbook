# Auto Annotator

The RedBrick AI Auto Annotator is an automated segmentation tool that allows teams to easily generate segmentation masks for hundreds of different structures on CT and MR images, which are then inserted into a Project pipeline as pre-labels.

To use Auto Annotator, you must have an [active Boost instance](./#creating-a-boost-instance) available in your Organization.

***

## Adding Auto Annotator to a Project

The decision to utilize Auto Annotator for a Project must be made **at Project creation.**&#x20;

After a Project has been created, there is no way to retroactively add Auto Annotator to it, as the model will be added to the Project pipeline as a pre-Stage.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.15.36@2x.png" alt="" width="563"><figcaption><p>An example pipeline with Auto Annotator</p></figcaption></figure>

If you have an active Boost instance in your Organization, you will notice that Step (4) of standard Project creation looks slightly different:

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.01.07@2x.png" alt="" width="563"><figcaption><p>Project creation with Auto Annotator</p></figcaption></figure>

1. The Auto Annotator toggle;
2. Object Label mapping window;
3. Model URL selection dropdown;

### Mapping Object Labels

After you've enabled Auto Annotator in a Project, you must map the labels that the algorithm will generate to a corresponding entry in your Redbrick Taxonomy.

Click on **Map object labels** to open the Mapping window.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.04.14@2x.png" alt=""><figcaption><p>The Mapping Window</p></figcaption></figure>

The Mapping Window allows you to:

1. Choose which Auto Annotator sub-type you would like to use for this specific Project;
2. Map the output of the designated model sub-type to the Object Labels of your Project's Taxonomy;

{% embed url="https://share.cleanshot.com/jpLLs897" %}
Mapping model output
{% endembed %}

Each entry in the Auto Annotator Labels list can only be mapped once. However, Taxonomy Labels can be mapped to as many structures as you'd like.

Consider the example below, where the model output for `kidney_right` and `kidney_left` are both mapped to a single RedBrick Object Label called `Kidney`.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.12.14@2x (1).png" alt=""><figcaption></figcaption></figure>

Once you have finished mapping your labels, click on **Save changes**.

### Selecting a Model

If you have multiple models integrated with RedBrick AI, you can use the dropdown field to select which model should run on this specific Project.

***

## Running Auto Annotator in a Project

Once your Project is created, any [data that you upload](../../importing-data/uploading-data-to-redbrick.md) or [integrate](../../importing-data/import-cloud-data.md) to the Project will automatically pass through the Auto Annotator pre-Stage, where automated annotation will occur.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.19.32@2x.png" alt=""><figcaption><p>4 Tasks in the Auto Annotator pre-Stage</p></figcaption></figure>

**There is nothing that the user needs to do for Tasks in the Auto Annotator pre-Stage.** After the Auto Annotator is done generating labels, the Task will automatically move to the next Stage in your Project pipeline.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.21.02@2x.png" alt=""><figcaption><p>Task History of a Task that was labeled automatically</p></figcaption></figure>

Once the Tasks have reached the next Stage in your pipeline, your team can begin work on it.
