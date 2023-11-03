---
description: Rapid & Collaborative Medical Data Annotation
---

# Getting Started

RedBrick AI is a purpose-built SaaS application created to help healthcare AI teams annotate medical data more effectively. RedBrick AI offers web-based annotation tools for CTs, MRIs, X-rays, etc., as well as comprehensive project management and quality control tools.

{% hint style="success" %}
Request a free trial or product demonstration by reaching out to us here - [https://redbrickai.com/contact](https://redbrickai.com/contact).
{% endhint %}

## Sample Project - Brain Brats

This guide will help you get started using RedBrick AI by showing you how to create a project from scratch.&#x20;

Let's get started!&#x20;

### Invite Your Team

RedBrick AI is a collaborative application built for engineers, clinicians and project managers. First, bring your team onto your annotation projects by adding them to your Organization.

{% content-ref url="organizations/what-is-an-organization.md" %}
[what-is-an-organization.md](organizations/what-is-an-organization.md)
{% endcontent-ref %}

{% embed url="https://www.loom.com/share/9cf245a1d06b4978b6822c7f3c31649f" %}

### Create a Taxonomy

Before creating a project, you have to create a labeling taxonomy that defines **what you will annotate** in your project. For this data set, we are going to annotate the following items:&#x20;

1.  Segment the following structures:&#x20;

    a. Edema

    b. Necrosis

    c. Enhancing Tumor

    d. Non-enhancing Tumor
2. Designate any Series that happens to be a low-quality image

{% content-ref url="projects/taxonomies/" %}
[taxonomies](projects/taxonomies/)
{% endcontent-ref %}

{% embed url="https://www.loom.com/share/3e41b8479a584a53ba953c963110e2ea" %}

### Create a Project

Now that you have formed your team and created a taxonomy, you can create your project by selecting the Brain Brats taxonomy and configuring your annotation workflow. We recommend a workflow with one Review Stage for the purposes of this demo.

{% embed url="https://www.loom.com/share/fac68e2510f8440b9d35b1e9a93d66e5" %}

### Upload the Brain Brats Data Set

We will use the sample MRI data set linked below for this demo.

{% embed url="https://drive.google.com/drive/folders/1_U_CRwS47tRwZCboUb8cdygeNaLmxw7P" %}
Sample MRI dataset
{% endembed %}

After downloading the data set, head over to the project you have created and click on the **Upload Data** button. Under the **Direct Upload** tab, select **NIfTI 3D Volume** as the data type, and select **Yes** for **Group Tasks by Study**.

Then, drag and drop the Brain Brats folder to the field and click on **Upload**.

{% embed url="https://www.loom.com/share/18f4fc466853459b9cfa43ce29b62f02" %}

If you'd like, you can also integrate your cloud storage to host your own data with RedBrick AI.

{% content-ref url="importing-data/import-cloud-data.md" %}
[import-cloud-data.md](importing-data/import-cloud-data.md)
{% endcontent-ref %}

### Begin Annotating

Nicely done - your project is now set up and ready for annotation! Open the annotation tool by clicking on the **Label** button on the top right of the project dashboard.

{% embed url="https://www.loom.com/share/9e97d5f48ba64a6a84cfe7e484130bfb" %}
