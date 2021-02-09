# Active Learning with Samsung SDS AutoLabel

This tutorial will walk you through how to use Samsung SDS AutoLabel to run an active learning workflow which can automate upto 80-90% of all manual labeling work required.  

{% hint style="info" %}
This Active Learning solution is currently in **Beta phase**, and will be available at [https://brightics.redbrickai.com](https://brightics.redbrickai.com). Currently the offering only supports **image bounding boxes,** but will be expanded to other label types soon. 

If you are interested in trying this solution, please write to us at [contact@redbrickai.com](mailto:contact@redbrickai.com)
{% endhint %}

## **What is Active Learning?**

The key idea behind active learning is that a machine learning algorithm can perform better with less labeled training data if it allowed to _choose_ the data from which it learns. An Active Learner interactively queries a human annotator to first label data points that it is uncertain about. \([Burr Seatles, Active Learning](https://www.morganclaypool.com/doi/pdf/10.2200/S00429ED1V01Y201207AIM018)\)  
  
Following this interactive and iterative process, you can label data _in order of information gain_ to the Active Learner, therefore eliminating the need to label data-points the _Active Learner can auto-label_. In practice, this approach is able to save 80-90% of manual labeling efforts required to label a dataset.  
  
Automation within this Active Learning framework is achieved in two different ways: 

1. Data points the Active Learner is already confident about don't have to be manually labeled by humans because they have already been accurately auto-labeled.  
2. Throughout the active learning iterations, the human annotator\(s\) will simply be _correcting_ low confidence predictions of the Active Learner. As time progresses, even the low confidence predictions of the Active Learner will require less and less corrections. Therefore, the average time spent to create a label reduces over time. 

{% hint style="success" %}
The **Active Learner** in this Active Learning workflow is the **Samsung SDS AutoLabel** algorithm. 
{% endhint %}

## Overview

Before diving into the step-by-step process of setting up your Active Learning project, let's have a look at what the workflow looks like, and understand what the different stages are, and their inner workings. 

![The basic Active Learning pipeline has 6 different stages.](../.gitbook/assets/2_1_input.png)

#### INPUT `[dataset-input]`

The first stage brings in data from the [Data Warehouse](../data-warehouse-1/overview.md) into your pipeline. 

#### TYPECAST `[type-cast]`

The `type-cast` is used in this pipeline to ensure this pipeline abides by the RedBrick AI pipeline framework rules - specifically, the two inputs into the `[brightics-aia-autolabel]` stage need to be the same i.e. `image_bbox`.

#### ACTIVE\_LEARNING `[brightics-aia-autolabel]`

The `[brightics-aia-autolabel]` stage is the core component of this Active Learning pipeline. This stage integrates with the Samsung SDS AutoLabel algorithm for training and generating predictions/confidence estimates.   
  
The `[brightics-aia-autolabel]` stage has two sub-components to it, which are described below:

1. **Task Queue.** The task queue contains all the data/labels queued in this stage, with the lowest confidence tasks at the top of the queue. Before AutoLabel has been trained and generated predictions with confidences, the queue is randomly sorted.  
2. **Training Set.** Tasks that have been manually labeled get added to the training set. AutoLabel is trained on this training set.

Within this stage, there are three possible actions which are covered below: 

1. **Send Batch.** The send batch action sends a batch of data, from the top of the task queue inside `[brightics-aia-autolabel]` , to the downstream `[manual-labeling]` step.  
2. **Trigger Training.** The trigger training action trains AutoLabel using the labeled data inside the training set. At the end of a training cycle, AutoLabel will generate predictions with confidence values on the task queue. The task queue will be re-ordered to have the least confident predictions at the top of the queue at the end of every training cycle.  
3. **Flush Tasks.** The flush task action sends all the tasks \(data and labels\) queued in `[brightics-aia-autolabel]` to the `[labelset-output]` stage to be stored in the Data Warehouse. 

#### LABEL `[manual-label]`

The manual labeling stage allows your team to manually label the data, or correct data that already has predictions on it. This step can be done collaboratively by inviting team members to your organization.

#### FEEDBACK `[feedback]`

The feedback step simply sends labeled tasks back to the `[brightics-aia-autolabel]` step to be added to the training set. 

**OUTPUT** 

Once tasks are flushed, the `[labelset-output]` stage stores all the data and labels in the Data Warehouse.



##  Set up your account

## Prepare your dataset

## Create the Active Learning Project

## 

