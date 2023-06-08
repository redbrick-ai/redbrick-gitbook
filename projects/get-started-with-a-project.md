# Get Started with a Project

## Creating a Project

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_team (4).png" alt=""><figcaption><p>Create project page</p></figcaption></figure>

To create a new Project, press the **Create Project** button on the Projects page.&#x20;

&#x20;Creating and setting up a Project can be done quickly and easily by following the steps below.

### Specify a Unique Project Name

Each Project has a unique name that can be changed at any time within Project Settings. &#x20;

### Select the Taxonomy for the Project&#x20;

Taxonomies are stored at the Organization level, which allows you to reuse a single labeling Taxonomy across Projects.

{% hint style="warning" %}
Selecting a Taxonomy for a Project is a permanent choice that cannot be undone. However, you can edit your Taxonomy after using it in a Project.
{% endhint %}

### Define your Project Workflow

Project workflows allow you to explicitly define a series of annotation and review steps in your project.&#x20;

You can also configure the **number of review stages** and the **review percentage** (i.e. randomly select a subset of data for review) in your workflow.&#x20;

Once data has successfully gone through all stages of your workflow, it will be stored in the **Ground Truth** Stage.&#x20;

A common workflow included a single Label Stage followed by two Review Stages where different sets of reviewers validate the annotations performed.&#x20;

{% hint style="info" %}
When a reviewer rejects a Task in a Review Stage, it is sent back to the Label Stage and automatically assigned to the same Labeler who annotated it the first time.
{% endhint %}

{% hint style="warning" %}
The number of Review Stages cannot be modified after a workflow has been created.&#x20;
{% endhint %}

## Additional Project Setup

Once you have successfully created a Project, you will most likely want to perform the following actions to add collaborators and data and modify Project settings.

### Adding Labelers to your Project

By default, all **Org Admins** have comprehensive access to all Projects. As with any elevated role, we recommend taking care when designating fellow team members as Org Admins.

Generally speaking, it's advisable to add Labelers and Reviewers to your Organization as **Org Members**. This grants them access to your Organization on the RedBrick AI Web Application, but limits their access and permissions.&#x20;

**Org Admins** have granular control over the Project-level access of all **Org Members**.

In order to add Labelers or Reviews to individual Projects, we advise the following:

1. On the Team Page, invite the Labeler/Reviewer as an **Org Member (MEMBER)**.&#x20;
2. After the Labeler/Reviewer accepts their invitation and creates an account, navigate to the Project you'd like to add them to and open the Workforce Tab. From there, you can invite the Labeler/Reviewer to the Project as either a **Project Admin** or **Project Member**. Please note that  if your Labeler/Reviewer is a **Project Admin**, they will have access to all Stages of a Project.&#x20;
3. If your Labeler/Reviewer is a **Project Member**, you can regulate their access to various Stages limited based on your workflow's needs or regulatory requirements.&#x20;

For a more in-depth breakdown of the permissions and access privileges associated with each role, please consult the documentation below.

{% content-ref url="../organizations/what-is-an-organization.md" %}
[what-is-an-organization.md](../organizations/what-is-an-organization.md)
{% endcontent-ref %}

### Uploading Data

You can upload data within a project either through the Web Application's UI or CLI/SDK. Most teams will [integrate external storage](../importing-data/import-cloud-data/creating-an-items-list.md) and host their own data, however, you can also [directly upload data to RedBrick AI servers](../importing-data/direct-data-upload.md).

If you have pre-annotated data or model-generated annotations, you can import them using our CLI/SDK.

{% content-ref url="../python-sdk/sdk-overview/importing-data-and-annotations.md" %}
[importing-data-and-annotations.md](../python-sdk/sdk-overview/importing-data-and-annotations.md)
{% endcontent-ref %}

### Assigning Tasks

Once you have uploaded data to your Project, RedBrick AI will begin automatically assigning Tasks to the users in your Project. You can learn more about the specifics of task assignment by reading on!

{% content-ref url="task-assignment.md" %}
[task-assignment.md](task-assignment.md)
{% endcontent-ref %}
