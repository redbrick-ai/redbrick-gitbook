---
description: >-
  RedBrick AI Projects are containers inside which you can manage all of your
  annotation and data processes.
---

# Overview

## Creating a Project

To create a project you can click on the Create Project button on the top left of the home screen, or the + button next to the Projects link on the left side bar.&#x20;

Creating a project requires the following:&#x20;

1. Selecting a data type:
   1. DICOM 3D: Allows you to upload and annotate 3D DICOM data for example, MRI, CT etc. This type supports NIfTI and DICOM.
   2. Image: Allows you to upload and annotate 2D RGB images of types png, jpeg, bmp etc.
   3. Video: Allows you to upload an annotate 2D RGB videos of type mp4, parsed image frames etc.
2. Annotation type
3. Taxonomy: The taxonomy configures your labeling interface and defines what categories you want to work with. See the [taxonomies](../data-labeling/taxonomies.md) documentation for more information.
4. Number of review stages: This defines your project pipeline and if/how many review stages you want.&#x20;

## What is a Pipeline?

The RedBrick AI pipelines are a framework that you can use to structure and automate your data efforts. You can think of the pipelines like a manufacturing assembly line where there is a product that goes through various discrete processes, that involve various automated and manual processes, before being completed.&#x20;

Similarly, pipelines are a production line for your data, where you can stitch together multiple stages based on configurable logic to run automated and manual processes to label your data.&#x20;

{% hint style="info" %}
Each project has **a single pipeline** associated with it, that defines the process of that project.&#x20;
{% endhint %}

![Example pipeline, with a single label stage followed by two review stages.](<../.gitbook/assets/image 501.png>)

You can see an example pipeline above, which involves a single labeling stage, followed by two review stages for quality assurance. The data you upload to the project, will flow through the pipeline following the logic laid out in the diagram. At each stage, a **task** is created and completed before moving to the next stage.&#x20;

## Project Dashboard

Your project dashboard contains all the information you need for managing your projects. Your project dashboard has a few sections:&#x20;

### Overview

The overview tab includes high level information regarding the status of your project.&#x20;

1. Tasks Overview - The status of data in your project
2. Project Pipeline - The basic framework of your project
3. Insights - Data plot conveying the total label & review tasks completed per day
4. Task Acceptance - Percentage rate of accepted against rejected tasks

![The overview page gives you a quick insight of the status of your project.](../.gitbook/assets/wide.png)

### Workforce

The workforce tab contains information about your team's progress & performance within a project.

1. Active Labelers - Gives you a project level overview and control over the team members
2. Labelling Productivity - View the total time and tasks _****_ completed over the last 30 days&#x20;

![](../.gitbook/assets/workforce.png)

### Data

The data page consists of all the tasks in a particular project. The filter system within the page further helps you to navigate across the different tasks based on type.

![](../.gitbook/assets/data.png)

View the section on importing data to understand how to import data into your project.&#x20;

{% content-ref url="importing-data/" %}
[importing-data](importing-data/)
{% endcontent-ref %}
