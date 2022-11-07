---
description: >-
  Continuously check that your labelers are maintaining high quality by having
  them relabel known ground truth.
---

# Labeler Evaluation

{% hint style="warning" %}
This feature is beta and we would love your feedback!
{% endhint %}

{% hint style="info" %}
Highlights

* Use benchmarks to train new labelers and make sure experienced labelers are staying focused.
* We recommend having a diverse set of more than 20 tasks to use to test your annotators.
* Mark ground truth tasks as benchmarks in the data tab, turn benchmarks on to test your annotators under project settings.
{% endhint %}

### Onboarding and training new labelers

Benchmarks can be used to onboard and train new annotators for a specific task without risking their early annotations becoming part of your ground truth or slowing down your review process.&#x20;

If you have benchmarks turned on, when a new annotator starts working on your project they will only be served known ground truth tasks to annotate. The annotations will get compared to the known ground truth to determine if they have successfully completed the task. Once they have successfully annotated enough tasks, only then will annotators be served unlabeled data to annotate.

### Keeping experienced annotators honest and focused

Even the most experienced annotators sometimes lose focus or forget the fundamentals of a labeling task. When you use benchmarks, annotators will randomly be assigned known ground truth tasks that will test that they are annotating correctly.&#x20;

If an annotator fails too many benchmark tests in a row (according to your settings) then they will be put back into training mode where they will need to successfully label benchmarks tests, just as if they were a new annotator. &#x20;

## Activating Benchmarks

1. Select which ground truth tasks you want to use to test your annotators. Go to the data tab in your project and filter for ground truth tasks. You can then select the star icon to select a given task. We recommend you select at least 20 tasks to get started, but a minimum of 3 are needed.
2. Go into your project settings and turn on the benchmarks feature.&#x20;
3. Adjust the settings for your requirements.&#x20;
