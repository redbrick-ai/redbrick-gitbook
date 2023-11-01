# Labeler Evaluation

### Calculating Labeler Quality Scores

RedBrick AI allows you to upload a Ground Truth annotation file alongside any image or volume file for the purposes of evaluating labeler quality.

This can be useful when you'd like to have RedBrick AI calculate a score that you can use to compare a specific labeler's performance against a known Ground Truth label set.&#x20;

### Blinded vs. Non-blinded Annotations

When evaluating labeler quality using these Evaluation Tasks, you have the option of allowing your labelers to visually reference the Ground Truth annotations that you are using as a baseline or keeping them invisible to the labeler.&#x20;

This feature is referred to as either **Non-blinded Annotations** or **Blinded Annotations,** respectively.

To create an Evaluation Task in RedBrick AI, you can take the following steps:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Sample Flow</p></figcaption></figure>

1. Upload your image/volume alongside your Ground Truth annotation file ("Baseline Annotations"). A walkthrough of how to do so can be found in our [documentation for importing annotations](../python-sdk/sdk-overview/importing-data-and-annotations.md#import-annotations).
2. After your Task has been created, determine whether you would like your labelers to see the Baseline while working. Navigate to your **Project Settings** and enable or disable the **Show reference annotations** toggle.&#x20;
   1. With the toggle enabled, labelers will be able to see the Baseline Annotations while working. With the toggle disabled, the Baseline Annotations will be invisible to the labeler.
   2. Please note that we also generally recommend disabling **Automatic Task Assignment** when testing labeler quality.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption><p>Relevant toggles in Project Settings</p></figcaption></figure>

3. Assign the Task to your labeler for completion.
4. After your labeler finalizes the Task, an agreement score will be displayed on the Data Page.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p>A completed Evaluation Task and score</p></figcaption></figure>
