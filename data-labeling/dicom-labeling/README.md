---
description: This guide covers details on using our DICOM annotation tool.
---

# DICOM Labeling

{% hint style="info" %}
Currently, this guide only covers use of our 3D DICOM annotation tool (CT scans, MRI etc.).
{% endhint %}

There are three main functions you can perform with the RedBrick AI DICOM tool - viewing, labeling, erasing. In this document we will cover all the functionality so that you will be an expert with the RedBrick AI tools.&#x20;

{% embed url="https://youtu.be/YpaiHrw8SLk" %}

## Layout

The first key thing to understand the layout of the tool. There are 4 core components to the layout (described in the image below).

* Left Sidebar: Your label/category actions will be here e.g. selecting a category of a segmentation, hiding/showing regions.&#x20;
* Top Bar: High level task actions e.g. submitting/accepting/rejecting tasks, creating comments etc.&#x20;
* Right Bar: Specific tools for drawing your annotations and viewing the images.&#x20;
* Canvas: The main view where the volume gets rendered and where you interact to create annotations.&#x20;

![DICOM Tool Layout](<../../.gitbook/assets/Group 495 (1).png>)

### Quad View

The default view of the volume is the quad view, which gives you a Multi-planar reconstruction view as well as a 3D reconstruction view.&#x20;

![Quad and primary view can be toggled on the right sidebar](<../../.gitbook/assets/Screen Shot 2022-01-12 at 3.30.40 PM.png>)

You can toggle between the Quad view and Primary view from the right sidebar or using the keyboard shortcuts.

| Shortcut | Action                 |
| -------- | ---------------------- |
| `P`      | Switch to primary view |
| `Q`      | Switch to quad view    |

### Primary View

The primary view is best if you want to focus on one plane. A single plane will make up the main view, and the orthogonal views and 3D reconstruction will be displayed on the right.&#x20;

![Primary view ](<../../.gitbook/assets/Screen Recording 2022-01-12 at 03.41.01 PM.gif>)

| Shortcut                        | Action                            |
| ------------------------------- | --------------------------------- |
| `double click` on view on right | Change main view to selected view |
| `shift` + `1`                   | Change main view to X view        |
| `shift` + `2`                   | Change main view to Y view        |
| `shift` + `3`                   | Change main view to Z view        |

## Navigating the volume

Now that you're well situated with the layout of the tool, let's describe how your view or navigate through the volume. From your right side bar, you can ensure you are in `view` mode so that all the functionality is available.&#x20;

![Change between modes and select tools from the right sidebar](<../../.gitbook/assets/Screen Shot 2022-01-12 at 4.08.23 PM.png>)

| Action                                                   | Shortcut                                                                                                                        |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Change to **view** mode to enable viewing functionality  | `V`                                                                                                                             |
| Change to **paint** mode to enable segmentation/painting | `Z`                                                                                                                             |
| Change to **erase** mode to enable segmentation erasing  | `X`                                                                                                                             |
| Enable the **cross-hair** viewing tool                   | `C`                                                                                                                             |
| **De-select** all annotations and enter view mode        | `esc`                                                                                                                           |
| **Zoom** into your volume in one of the 2D views         | <p><code>right click</code> + <code>drag</code> </p><p>or<br><code>ctrl</code> + <code>scroll</code></p>                        |
| **Pan** across your volume in one of the 2D views        | <p><code>middle click</code> + <code>drag</code> <br>or<br><code>shift</code> + <code>left click</code> + <code>drag</code></p> |
| **Change slice** in 2D view                              | `scroll`                                                                                                                        |
| **Reset views** to original configuration                | `spacebar`                                                                                                                      |

### Cross-hair tool

Using the cross-hair tool you can synchronize all the views to view particular parts of your volume in different planes.&#x20;

![Cross-hair tool in quad view](<../../.gitbook/assets/Screen Recording 2022-01-12 at 04.15.21 PM.gif>)

### **3D viewing**

The 3D view of your image can be enabled on the bottom right of your screen. Once enabled, you can interact with your 3D volume using the following actions.&#x20;

| Actions                                | Shortcut                        |
| -------------------------------------- | ------------------------------- |
| **Rotate** the volume                  | `left click` + `drag`           |
| **Zoom** into your volume              | `scroll`                        |
| **Pan** across your volume             | `shift` + `left click` + `drag` |
| **Rotate** the volume **in the plane** | `ctrl` + `left click` + `drag`  |

![Interacting with your 3D volume](<../../.gitbook/assets/Screen Recording 2022-01-12 at 04.22.01 PM.gif>)

### Windowing

To better view your volume in 2D and 3D, you can set the window width and center to display a certain range of image intensity values. The window panel is **collapsed** by default, but can be expanded on the _right side bar._&#x20;

| Actions                 | Shortcuts                                     |
| ----------------------- | --------------------------------------------- |
| Change **window width** | `ctrl` + `left click` + `drag` (horizontally) |
| Change **window level** | `ctrl` + `left click` + `drag` (vertically)   |

## Segmentation

With our segmentation tool you can perform semantic segmentation or instance segmentation. Please view the video below for a quick explanation of how you can create, edit, and delete your segmentations.&#x20;

{% embed url="https://youtu.be/IuErW7g1X4M" %}

Now, let's cover some details of the specific tools.&#x20;

### Paint brush

The brush tool allows you to segment your volume with a 2D circular brush or a 3D spherical brush.    You can edit the size of the brush and toggle 2D/3D on the right tool bar.      &#x20;

| Actions                                    | Shortcuts                                                                                                                                        |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Toggle between **2D** and **3D**           | `d`                                                                                                                                              |
| **Increase** and **decrease brush size**   | `w` and `s`                                                                                                                                      |
| **Painting**                               | `left click` and `drag` (in paint mode)                                                                                                          |
| **Erasing**                                | <p><code>right click</code> and <code>drag</code> (in paint mode)</p><p>and<br><code>left click</code> and <code>drag</code> (in erase mode)</p> |
| Create a **new** segmentation **instance** | `tab`                                                                                                                                            |
| **Deselect all labels**                    | `esc`                                                                                                                                            |
| **Delete** a **selected** **label**        | `backspace`                                                                                                                                      |

### Pen and Scissor Tools

The pen and scissor tools give you finer control over creating and editing annotations. Using these tools you can draw a free-hand polygon that will be converted to a 2D or 3D segmentation.&#x20;

![](<../../.gitbook/assets/Screen Recording 2022-01-12 at 07.29.39 PM.gif>)

| Actions                                           | Shortcut                                                                                          |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Add** a single **node** with **pen tool**       | `left click` (in paint mode)                                                                      |
| Create a **free-hand shape** with **pen tool**    | `left click` + `drag` (in paint mode)                                                             |
| **Add a single node** with **scissor tool**       | <p><code>left click</code> (in erase mode)<br>and<br><code>right click</code> (in paint mode)</p> |
| Create a **free-hand shape** with **eraser tool** | `left click` + `drag` (in erase mode)                                                             |

### Thresholding

To help automatically segment only a portion of intensity values, you can define a threshold on both the pen/scissor and brush tools.&#x20;

![](<../../.gitbook/assets/Screen Recording 2022-01-12 at 08.04.58 PM.gif>)
