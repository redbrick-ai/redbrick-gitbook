---
description: Glossary of important concepts and definitions.
---

# Core Concepts

## Organizations

Organizations are containers within which all your assets live. Permissions and collaboration are handled within organization i.e. you can create an organization and add members to collaborate with. 

## Datasets and Labelsets

Datasets and labelsets are simply named containers for raw data and labels. You can use datasets or labelsets as an input to projects - if you use a labelset as an input to a project, it will begin with already labeled data. 

## Projects

Projects will acts as your home base for labeling efforts. Projects orchestrate your labeling efforts, and usually start with datasets containing raw data, and end with labelsets containing your labels. Each project has a single pipeline associated with it The process in between raw data and labeled data in a project is defined by how you build your pipeline.  

## Pipelines

Pipelines define how your labeling efforts are structured. Each project has a pipeline associated with it - a single data point flowing through a pipeline is called a **task.**   
  
The individual modules that are used to construct a pipeline are called **bricks**. When a brick is added to a pipeline and its settings are configured, it is called a **stage.** 

## Task Event

A single task event is a single datapoint \(one image or one video\) going through a single stage in a pipeline. If you have a pipeline containing 3 stages, and 100 data points will go through all 3 stages, this project will have 300 task events. 

## 

