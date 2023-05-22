# 3D Slicer Integration

3D Slicer can be integrated into your RedBrick AI work flows for a smoother annotating experience.&#x20;

You can now export Tasks from RedBrick AI to 3D Slicer, complete annotation work within 3D Slicer, and all changes will be automatically synchronized to the RedBrick AI web application.&#x20;

{% hint style="info" %}
Current Version, v0.1.3:

* Both 3D DICOM and NIfTI images are supported
* Annotations can only be created with the 2D/3D Brush Tool
* Multi-series images are not supported
* RedBrick AI Taxonomies are supported, (3D Slicer Taxonomies are not)
* Consensus Projects are not supported

Our roadmap includes plans to expand the functionality of this integration in the near future.
{% endhint %}

### Setup

#### Enable the 3D Slicer Integration

By default, the integration with 3D Slicer is disabled for all Organizations. If you would like to enable this integration for your Organization, please reach out to us at [contact@redbrickai.com](mailto:contact@redbrickai.com).

#### Perform First-Time Setup

After confirming that the 3D Slicer integration has been enabled for your Organization, launch 3D Slicer (or download and install it if you haven’t already) and open the Python Console.

Within the Python Console, enter the following command: `pip_install('redbrick-slicer -U')`

Note: the above pip command will also install the latest version of redbrick-slicer&#x20;

Please see the following video for a brief visual overview of the first-time setup process

{% embed url="https://www.loom.com/share/9272c377d860499ab5c28595adae9ede" %}
Visual walkthrough of installing redbrick-slicer within 3D Slicer
{% endembed %}

### Annotating

#### Import a Task from RedBrick

In the RedBrick AI web application, navigate to the Data Page of one of your Projects. Now that your Organization has the 3D Slicer integration enabled, you will see a new button next to the **Open in Editor** button.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-18 at 15.42.16.png" alt=""><figcaption><p>The "Copy command to 3D Slicer" button within a Project's Data Page</p></figcaption></figure>

</div>

Click on this **Copy command to 3D Slicer** button to copy the 3D Slicer import command for a specific Task to your clipboard.

{% hint style="warning" %}
A Task has to be _assigned to you_ in order for it to open in 3D Slicer.
{% endhint %}

Next, navigate to 3D Slicer, paste the import command into the Python Console, and press **Enter**.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-18 at 16.10.03.png" alt=""><figcaption><p>A successful Task import</p></figcaption></figure>

A successful import will display your Project Taxonomy, any Segmentations within that Taxonomy, as well as the Task ID.

In order to start annotating, the following steps must be adhered to strictly:

1. Confirm that the "Segmentation" and "Source volume" fields are correct. Both of these fields should auto-populate, so it's best to avoid configuration here or interacting with the other dropdown menu options.
2. Click the **Add** button to generate a Slicer Segmentation.
3. Click on the colored square next to the Segmentation Name to open the **Terminology** dialog box. Within the **Terminology** box, you can confirm that you have correctly selected your Project's Taxonomy and choose a Segmentation to begin annotating.
4. Annotate your images - (we recommend saving frequently!)
5. Click on the **Save** button when your annotations are complete to export the Segmentations to RedBrick AI.
6. Return to the RedBrick AI web application to view the Segmentations you created in 3D Slicer.

You can find a walkthrough of importing a Task, annotating it, and exporting it back to RedBrick AI below.

{% embed url="https://www.loom.com/share/8ce52de168234e468b1a915123e90f05" %}

{% hint style="danger" %}
This integration **only supports Segmentations created in RedBrick AI Taxonomies**. Any Segmentation types created in Slicer will not display in the RedBrick Annotation Tool and may lead to format errors upon further export.
{% endhint %}





\
