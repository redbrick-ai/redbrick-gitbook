---
description: >-
  RedBrick AI Projects are containers inside which you can manage all of your
  annotation and data processes.
---

# Overview

Projects are mainly defined by the following: 

1. The type of data you're working with `image` or `video`
2. The type of labels you're working with `bounding box` , `segmentation` etc. \(see [this](../data-labeling/overview.md) for a complete list of supported label types.\) 
3. The [project pipeline](overview.md#what-is-a-pipeline).
4. The project raw data. 

## What is a Pipeline?

The RedBrick AI pipelines are a framework that you can use to structure and automate your data efforts. You can think of the pipelines like a manufacturing assembly line where there is a product that goes through various discrete processes, that involve various automated and manual processes, before being completed. 

Similarly, pipelines are a production line for your data, where you can stitch together multiple stages based on configurable logic to run automated and manual processes to label your data. 

{% hint style="info" %}
Each project has **a single pipeline** associated with it, that defines the process of that project. 
{% endhint %}

{% hint style="info" %}
**What is a task?**

Each datapoint that you upload into your project is created into a **task** inside a stage. Each task can have the following states: 

1. `ASSIGNED -` Assigned to a user, for example a labeling or review task. ``
2. `UNASSIGNED -` Queued in the stage, but currently not assigned to any user.
3. `COMPLETED -` Has finished processing through the stage.
4. `IN PROGRESS -` Is currently going through the stage, e.g. when a user saves a labeling task, it gets marked `IN PROGRESS`.
{% endhint %}

![Example pipeline, with a single label stage followed by two review stages.](../.gitbook/assets/screen-shot-2021-06-21-at-7.15.55-pm.png)

You can see an example pipeline above, which involves a single labeling stage, followed by two review stages for quality assurance. The data you upload to the project, will flow through the pipeline following the logic laid out in the diagram. At each stage, a **task** is created and completed before moving to the next stage. 

## Project Dashboard

Your project dashboard contains all the information you need for managing your projects. Your project dashboard has a few sections: 

### Overview

The overview tab includes high level information regarding the status of your project. 

![Project dashboard overview.](../.gitbook/assets/group-467-2-.png)

### Workforce

The workforce tab contains information about your team's progress and performance within a particular project. Specifically, you can view the total _tasks ****_completed over the last 30 days. 

![Manage your team progress and performance from the workforce tab](../.gitbook/assets/screen-shot-2021-06-21-at-7.47.08-pm.png)

### Data

You can interact with your data inside the data tab. 

![Interact with your data in the project dataset tab.](../.gitbook/assets/app.redbrickai.com_3d0caac7-b1e9-483f-8676-c0aca73af232_orgsettings-4-.png)

View the section on importing data to understand how to import data into your project. 

{% page-ref page="importing-data/" %}

