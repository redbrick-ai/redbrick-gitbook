# Boost

Boost is the engine that powers several of RedBrick AI's automated segmentation and AI-assisted tools, including:

* [F.A.S.T.](../../annotation-and-viewer/segmentation/segmentation-tools.md#fast-automated-segmentation-tool-f.a.s.t);
* the [Mask Propagation Tool](../../annotation-and-viewer/segmentation/segmentation-tools.md#mask-propagation-tool);
* [Auto Annotator](auto-annotator.md) (formerly CT Segmentator);

***

## Enabling Boost for Your Team

All of the tools powered by Boost require an active instance ("runner"). All instances of Boost can be created, deleted, enabled ("started"), and disabled ("stopped") by Org Admins and Org Owners at any time, and these instances **are priced separately from the standard pricing model.**

### Creating a Boost Instance

To create an instance, navigate to the Boost Page in the lefthand sidebar. Then, on the Boost Page, click on **Create Instance**.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 15.51.58@2x.png" alt=""><figcaption><p>Creating an instance</p></figcaption></figure>

The **Model Image** field is reserved for cases where your team has configured and integrated your segmentation model with RedBrick, i.e. if you're bringing your own model to the platform.

If you are not using this **Bring Your Own Algorithm** approach and wish to use RedBrick's model, you should leave the **Model Image** field empty.

After selecting a region, choose the amount of CPUs/memory that your instance will have by clicking on the corresponding blue **Create** arrow.

Congratulations! Your Boost instance has been created and will be active shortly. In the meantime, you will be redirected to your Boost Dashboard, which shows the status of your newly created instance.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-16 at 14.40.20@2x (1).png" alt=""><figcaption><p>The RBAI Boost Dashboard</p></figcaption></figure>

**Please note** that it often takes anywhere from 3-20 minutes for a newly created Boost instance to fully activate.

***

### Stopping and Starting an Instance

If you'd like to temporarily pause your Boost instance, simply click **Stop** for the instance on the Boost Dashboard.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.23.09@2x.png" alt="" width="281"><figcaption></figcaption></figure>

The instance will then gain the Stopping status until it is fully paused.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.33.06@2x (1).png" alt="" width="266"><figcaption></figcaption></figure>

You can then click on **Start** to reactivate the instance.

***

### Deleting an Instance

All Boost instances will be considered active unless disabled or deleted by a RedBrick user. If you are not actively using the tools the Boost provides, we recommend deleting all instances.

To delete a Boost instance, simply click on the red trash can on the right side of the Boost Dashboard.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-16 at 14.51.22@2x.png" alt=""><figcaption><p>Deleting an instance</p></figcaption></figure>

