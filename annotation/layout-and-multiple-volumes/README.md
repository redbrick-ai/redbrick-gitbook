# Layout & Multiple Volumes

The RedBrick AI annotation tool layout can be customized to display your volume(s) as needed. If your tasks have multiple series, you can view all the series together, along with MPR, 3D, and MIP views.

{% hint style="info" %}
The layout is configurable only with 3D images, or when there is more than 1 series in your task.
{% endhint %}

## Default Layout

For tasks with a single series, the annotation tool will be in MPR (Multi-planar Reconstruction) mode by default. &#x20;

<figure><img src="../../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_2212c7b4-ec28-4fc3-8797-c516ac3389e1_tool_Label_taskid=22f76c14-82e7-4d2a-aaf1-bd05afd3ea7c.png" alt=""><figcaption><p>Multi-planar reconstrution layout for a single series</p></figcaption></figure>

For tasks with multiple series, the annotation tool will display all the imaging plane for all series (up to 9).&#x20;

<figure><img src="../../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_2212c7b4-ec28-4fc3-8797-c516ac3389e1_tool_Label_taskid=22f76c14-82e7-4d2a-aaf1-bd05afd3ea7c (1).png" alt=""><figcaption><p>Axial plane displayed for all four series</p></figcaption></figure>

You can modify the default layout for a project using hanging protocols.&#x20;

{% content-ref url="custom-hanging-protocol.md" %}
[custom-hanging-protocol.md](custom-hanging-protocol.md)
{% endcontent-ref %}

## Modifying your layout

In the Layout context panel, you will be able to select your view layout - you can display up to 9 volumes/reconstructions at once. When the Layout settings are toggled, you can drag and drop series/reconstructions from the context panel to construct your viewports.&#x20;

{% embed url="https://www.loom.com/share/0d4544a277264a4099fc19bdc5fc6461" %}
Configuring your annotation layout
{% endembed %}

## Multi-planar Reconstruction

You can toggle multi-planar reconstruction for any volume using the actions dropdown on the viewport. Toggling the MPR mode will re-adjust your layout to display a single volume with its reconstructions. You can also manually drag and drop the reconstructed views from the Layout Context Panel.

<figure><img src="../../.gitbook/assets/Screen Shot 2022-10-24 at 4.57.25 PM.png" alt=""><figcaption></figcaption></figure>

#### Crosshairs

Once in MPR mode, activate **crosshairs** from the topbar, or with the `c` shortcut to synchronize the reconstructed views.&#x20;

<figure><img src="../../.gitbook/assets/ezgif.com-gif-maker (6).gif" alt=""><figcaption></figcaption></figure>

## Max/Min Intensity Projection (MIP)

Maximum intensity project takes several slices of 3D data and merges them together. This feature is available as a separate viewport.

#### Activating MIP

Open the layout panel -> Click a series to expand the view options, the MIP option is at the bottom, you can drag it onto a viewport.

{% embed url="https://www.loom.com/share/d4c0cbb5e16347b4890209e77636d503" %}

#### Using MIP

Once activated, you will not be able to paint or draw labels here, but you will be able to use this a reference visualization for annotating the main view. MIP is only available along the imaging axis (not with MPR). Use the slider on the viewport to adjust the slab thickness.&#x20;
