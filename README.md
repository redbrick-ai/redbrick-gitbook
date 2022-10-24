---
description: Training Data, Made Easy.
---

# Getting Started

RedBrick AI is a purpose-built SaaS application to help healthcare AI teams in annotating medical data. RedBrick AI offers web-based annotation tools for CT, MRI, X-ray, etc., and comprehensive project management and quality control tools.&#x20;

{% hint style="success" %}
Request a free trial, or product demonstration by reaching out to us here - [https://redbrickai.com/contact](https://redbrickai.com/contact).
{% endhint %}

## Sample Brain Brats Project

To get started with using RedBrick AI, follow along with this guide in creating a project from scratch. For the purposes of this example, we will use the Brain Brats MRI dataset linked below (NIfTI files).&#x20;

{% embed url="https://drive.google.com/drive/folders/1_U_CRwS47tRwZCboUb8cdygeNaLmxw7P" %}
Sample MRI dataset
{% endembed %}

### Invite your team

RedBrick AI is a collaborative application used by engineers, clinicians, and project managers. You can start involving your entire team in your annotation projects by first adding them to your organization.

{% content-ref url="organizations/what-is-an-organization.md" %}
[what-is-an-organization.md](organizations/what-is-an-organization.md)
{% endcontent-ref %}

{% embed url="https://www.loom.com/share/9cf245a1d06b4978b6822c7f3c31649f" %}

### Create a taxonomy

Before creating a project, you have to create a labeling taxonomy that defines **what you will annotate** in your project. For this dataset, we are going to annotate the following items:&#x20;

1. Segment the following structures:&#x20;
   1. Edema
   2. Necrosis
   3. Enhancing Tumor
   4. Non-enhancing Tumor
2. Classify any series that is a bad-quality image

{% content-ref url="projects/taxonomies/" %}
[taxonomies](projects/taxonomies/)
{% endcontent-ref %}

{% embed url="https://www.loom.com/share/3e41b8479a584a53ba953c963110e2ea" %}

### Create a project

Now that you have invited your team and created a taxonomy, you can create your project by selecting the Brain Brats taxonomy, and configuring your annotation workflow. For this exercise, we recommend a workflow with 1 Review stage.&#x20;

{% content-ref url="projects/get-started-with-a-project.md" %}
[get-started-with-a-project.md](projects/get-started-with-a-project.md)
{% endcontent-ref %}

{% embed url="https://www.loom.com/share/fac68e2510f8440b9d35b1e9a93d66e5" %}

### Upload the Brain Brats dataset

First, download the Brain Brats dataset linked above. After downloading, head over to the project you have just created and click on the **Upload Data button.** Within the upload data dialog, select **NIfTI 3D Volume** as the data type, and select **Yes for Group by Study.** Then, drag and drop the Brain Brats folder and click on Upload.

{% embed url="https://www.loom.com/share/18f4fc466853459b9cfa43ce29b62f02" %}

For your information, you can integrate your cloud storage to host your own data with RedBrick AI.&#x20;

{% content-ref url="importing-data/import-cloud-data.md" %}
[import-cloud-data.md](importing-data/import-cloud-data.md)
{% endcontent-ref %}

### Begin Annotating

Your project is completely set up and ready for annotation! Open the annotation tool by clicking on the Label button on the top right of the project dashboard.&#x20;

{% embed url="https://www.loom.com/share/9e97d5f48ba64a6a84cfe7e484130bfb" %}
