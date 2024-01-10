# Viewer Basics

RedBrick AI is designed for native medical image viewing and annotation, supporting all radiology modalities. The platform supports X-ray, CT, MRI, Ultrasound, and other 2D, 3D, and video modalities.

<figure><img src="../../.gitbook/assets/RedBrick AI 2024-01-10 at 12.13.14@2x.png" alt=""><figcaption></figcaption></figure>

There are 4 main components to the annotation interface. We will refer to each of these components throughout the documentation.

1. **Left sidebar** is where you create, edit, and interact with annotations and attributes.
2. **Top bar** contains Task-level actions such as task submission and saving and the environment settings (Windowing, Layout), [Version Explorer](../creating-editing-and-deleting-annotations.md#annotation-version-explorer), [Segmentation Tools](../segmentation/#segmentation-and-other-tools), and Quick Measurement Tools.
3. **Context panel** shows additional information and settings for any currently selected tool(s).
4. **Main canvas** is where you interact with your images and apply your annotations to your images/volumes.

## Viewing and navigating through your volume

Interacting with your images in RedBrick AI is similar to other medical imaging & PACS viewers. This section covers the basic shortcuts and functions for navigating through a volume.

{% hint style="info" %}
You can find key shortcuts [by clicking on the (?) Help button](https://share.redbrickai.com/R7rLT17M) on the bottom right.
{% endhint %}

### Changing slices

1. **Scroll:** Scroll over any of the viewports.&#x20;
2. **UI:** Use the [viewport's slider or up/down slice buttons](https://share.redbrickai.com/CKSfZHCn).&#x20;
3. **Shortcut:** Use the `up arrow` and `down arrow` keyboard shortcuts on the selected viewport.&#x20;
4. **Quick slice change:** Hold `alt`/`option` and `left click` `drag` to quickly change slices.

### Zoom and pan

1. **Zoom:** Hold `ctrl` and `scroll` to zoom.&#x20;
2. **Quick zoom:** Hold `ctrl` and `right click` `drag` for a quick zoom.
3. **Pan:** Hold `shift` and `left click` `drag` to pan.&#x20;

### **Windowing**

1. **UI:** Adjust windowing [on the context panel by activating it](https://share.redbrickai.com/Rp5RcGGN) from the top bar.
2. **Shortcut:** Hold `ctrl` and `left click` `drag` vertically to adjust the level and horizontally to adjust the width.

### 3D model viewing

1. **Rotate**: `Left click` `drag` to rotate the volume in 3D.&#x20;
2. **Rotate fixed plane**: Hold `ctrl` and `left click` `drag` to rotate the model fixed in the plane.&#x20;
3. **Pan**: Hold `shift` and `left click` `drag` to pan.&#x20;
4. **Zoom**: Hold `ctrl`/`cmd` and `scroll` to zoom.&#x20;

{% embed url="https://share.redbrickai.com/QMZlvrSJ" %}
Basic viewing interactions.
{% endembed %}

1. **Rendering preset**: adjusts the photorealistic rendering style.&#x20;
2. **Shift**: adjusts the volume rendering transfer function to modify the rendering.&#x20;
3. **Maximum opacity:** sets the maximum voxel opacity of the rendered image.&#x20;

{% embed url="https://share.redbrickai.com/ytY3Qyg6" fullWidth="false" %}
Basic windowing functions.
{% endembed %}

### Crosshairs and oblique plane

Crosshairs will synchronize multiple projections of a single volume. Oblique planes allow you to view a non-orthogonal view of a volume.&#x20;

{% hint style="info" %}
Crosshairs will only be available on 3D modalities. Also, you must have multiple orthogonal projections in your viewport (for example, Axial and Sagittal) for cross-hairs to appear.&#x20;
{% endhint %}

#### Crosshairs

1. **Activate**: [From the top bar](https://share.redbrickai.com/2S9DVjnD) or by pressing `c`.&#x20;
2. **Deactivate:** [From the top bar ](https://share.redbrickai.com/2S9DVjnD)or by pressing `esc`. By default, deactivated crosshairs will be shown on the canvas and can be reactivated by selecting them. To hide deactivated cross-hairs press `cmd/ctrl` `shift` `c`.&#x20;

#### Oblique plane

1. **Activate**: `Right click` on any viewport, then select `activate oblique`. This will enable an oblique plane for just the selected projection.
2. **Usage**: The oblique plane crosshair for each viewport will be color-coded. For example, the Sagittal oblique plane is purple in the video below. Rotating the purple crosshair creates an oblique plane on the Sagittal view.&#x20;

{% embed url="https://share.redbrickai.com/jjCnK3MT" %}
Using crosshairs and oblique planes.
{% endembed %}

### Maximum and minimum intensity projection (MIP)

Maximum Intensity Projection (MIP) displays the highest intensity values in a 3D image along a viewing axis, useful for highlighting bright structures like blood vessels. Minimum Intensity Projection shows the lowest values, useful for revealing dark structures like airways.

{% hint style="info" %}
You can only view MIP along the imaging axis for any volume.&#x20;
{% endhint %}

To **activate,** change the displayed view to MIP in any viewport using the view dropdown on the top left.

{% embed url="https://share.redbrickai.com/M8bQSW5f" %}
Displaying MIP.
{% endembed %}

***

## Managing your layout

RedBrick AI's viewer is flexible in how it displays series. You can customize the layout manually or use [hanging protocols](custom-hanging-protocol.md) to display single or multiple series.&#x20;

### Changing layout and displaying series

1. **Change layout grid:** Each modality has a default layout grid [which can be modified from the layout grid](https://share.redbrickai.com/35RfQGH2) on the top bar. The viewer supports everything between 1x1 and 3x3, showing a maximum of 9 views.
2. **Displaying series:** You can customize what is shown in each viewport; this can be any 2D or 3D view.&#x20;
   *   **Drag and drop:** You can drag and drop any series or projection from the layout context panel to a target viewport.&#x20;

       <div align="center" data-full-width="true">

       <figure><img src="../../.gitbook/assets/RedBrick AI 2024-01-10 at 16.02.15.gif" alt=""><figcaption><p>Drag and drop.</p></figcaption></figure>

       </div>
   *   **Viewport selector:** You can use the dropdown on any viewport to cycle between projections of that series.

       <figure><img src="../../.gitbook/assets/RedBrick AI 2024-01-10 at 16.03.32.gif" alt=""><figcaption><p>Viewport selector.</p></figcaption></figure>
   *   **Quick change:** You can hover over the thumbnails on the layout context panel to directly place the view in the corresponding layout position.

       <figure><img src="../../.gitbook/assets/RedBrick AI 2024-01-10 at 16.07.27 (1).gif" alt=""><figcaption><p>Quick change.</p></figcaption></figure>
3.  **Maximize and minimize view:** When you have more than 2 views displayed, you can maximize 1 viewport so that it's larger than the rest. Pressing `enter` will expand the currently selected viewport. Alternatively, you can `right click` and select `maximize viewport` on the layout menu.\


    <figure><img src="../../.gitbook/assets/RedBrick AI 2024-01-10 at 16.12.09.gif" alt=""><figcaption></figcaption></figure>
4. **Full-screen mode:** [Press `f` to enter full-screen mode](https://share.redbrickai.com/Q28P1X0m) for distraction-free annotation.

### Multiplanar reconstruction (MPR)

1. **Manually:** You can create an MPR view by manually configuring the viewport and selecting the projections of your series [following the instructions above](./#changing-layout-and-displaying-series).
2. **Right-click menu:** You can also display an MPR view by `right click` on the viewport and selecting `MPR layout`. This will [create a new layout tab](./#creating-multiple-layout-tabs) with the MPR view.

### Creating multiple layout tabs

Often you may want to move between two pre-set viewing configurations. For example, between a large 3D view and a view of all projections - Sagittal, Coronal, and Axial. This can be accomplished by creating multiple layout tabs.&#x20;

{% embed url="https://share.redbrickai.com/Hy6gjRL8" %}
Creating multiple layout tabs
{% endembed %}
