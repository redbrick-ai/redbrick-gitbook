# Get started with a project

To create a new project, press the "Create Project" button on the Projects page. There are a few simple steps to creating and setting up a project.&#x20;

## Creating a project

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_team (4).png" alt=""><figcaption><p>Create project page</p></figcaption></figure>

### Specify a unique project name

Each project has a unique name that can be changed at any time within Project Settings. &#x20;

### Select the taxonomy for the project&#x20;

Taxonomies are stored at the _Organization_ level. This allows you to reuse the same labeling taxonomy across projects.

{% hint style="warning" %}
Once you select a taxonomy for your project, you cannot change the taxonomy. However, you can edit your taxonomy after using it in a project.
{% endhint %}

### Define your project workflow

Project workflows allow you to explicitly define a series of annotation and review steps in your project. You can configure the **number of review stages** and the **review percentage** (randomly select a subset of data for review) in your workflow. Once data has successfully gone through all stages of the workflow, it will be stored in the **ground truth** stage.&#x20;

A common pattern used is to have a single annotation stage, followed by two Review stages where different sets of reviewers validate the annotations performed.&#x20;

{% hint style="info" %}
When a reviewer rejects a task in a review stage, it is sent back to the label stage and automatically assigned to the same annotator who annotated it the first time.
{% endhint %}

{% hint style="warning" %}
The number of review stages cannot be modified after the workflow has been created.&#x20;
{% endhint %}

## Additional project set up

Once you have successfully created a project, you will most likely want to perform the following actions to add collaborators and data and modify project settings.

### Adding labelers to your project

All admins have access to all projects by default. You can manually add Labelers to individual projects and **assign them as Labelers or Reviewers**. Please read the following section for more details:

{% content-ref url="../organizations/what-is-an-organization.md" %}
[what-is-an-organization.md](../organizations/what-is-an-organization.md)
{% endcontent-ref %}

### Uploading data

You can upload data within a project either through the UI or CLI/SDK. Most teams will [integrate external storage](../importing-data/import-cloud-data/creating-an-items-list.md) and host their own data, however, you can also [directly upload data to RedBrick AI servers](../importing-data/direct-data-upload.md).

If you have pre-annotated data, or model-generated annotations, you can import them using our CLI/SDK.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### Assigning tasks

Once you have uploaded data to your project, RedBrick AI will begin automatically assigning tasks to the users in your project. Please read more about task assignment here:&#x20;

{% content-ref url="how-task-assignment-works.md" %}
[how-task-assignment-works.md](how-task-assignment-works.md)
{% endcontent-ref %}
