# Overview

The RedBrick AI DICOM annotation tool is a web-based annotation tool with native support for DICOM medical images. The solution supports 2D and 3D data and allows for segmentation, classification, and vector annotations.&#x20;

## Interface overview

![](<../.gitbook/assets/Group 28384.png>)

There are 4 main components to the annotation interface:

1. The Left Sidebar: This is where you create, edit and interact with annotations and attributes.&#x20;
2. The Top Bar: The top bar contains task level actions like task submission, and tools like windowing and segmentation tools.&#x20;
3. The Context Panel: This panel shows additional information and settings for the currently **selected** tools.
4. The Main Canvas: This is where you will interact with your images and perform annotations.&#x20;

## Navigating your volume

If you've used other DICOM viewers, you may already be familiar with navigating through volumes on RedBrick AI

* **Changing slices:** Change slices by scrolling on any of the viewports. You can also use the slider on the left side of each view port to move through the volume quickly. Using the `up arrow`  and `down arrow`  keys will change one slice at a time on the selected viewport.
* **Zoom:** Zoom into your volume by holding `control + scroll`
* **Pan:** Pan around your volume by doing `shift + left click drag`
* **Crosshairs:** Synchronize re-constructions of the same series by enabling the cross hair tool on the top bar. This is only available when you have 3 orthogonal reconstructed views (Sagittal, Coronal, and Axial)
* **Reset:** To reset all views to the default state (center slice and neutral zoom) press `spacebar`
* **3D view:** The 3D view of your image can be enabled on the bottom right of the 3D view port. Once enabled, you can interact with your 3D volume using the following actions.
  * **Rotate** the volume`left click` + `drag`
  * **Zoom** into your volume`scroll`
  * **Pan** across your volume`shift` + `left click` + `drag`
  * **Rotate** the volume **in the plane** `ctrl` + `left click` + `drag`
* **Windowing:** Modify the window width and level by holding `control + left click drag`
* **Min / Max viewport:**  With a 2x2, 2x3, or 3x2 layout configuration toggle min/max by pressing `enter` or `return`
* **Change selected viewport:** The selected viewport is the viewport that you last clicked in, or you can navigate through by using `shift + arrow keys`. This can be combined with min/max to quickly explore your views.

## How tasks work with DICOM annotation

On RedBrick AI, a single task is a single unit that moves through the annotation workflow. A single task is served to annotators/reviewers to complete in one session.&#x20;

Typically, there will be a 1-1 mapping between a **DICOM series** and a RedBrick AI task. If you have 1,000 series, the typical use case would result in 1,000 tasks in the RedBrick AI annotation workflow.&#x20;

You can choose to create a multi-series task i.e. have a 1-1 mapping between a **DICOM study** and a RedBrick AI task.&#x20;

### Single Series Task

When uploading your [items list](../importing-data/import-cloud-data/creating-an-items-list.md#items-list-format), this is the structure to follow for creating a single-series annotation task (only one series per items entry). The following structure will create **two tasks on RedBrick AI**, with each task having a **single series only**.&#x20;

```json
[
  {
    "items": ["path/to/series001.nii"]
  },
  {
    "items": [
      "path/to/series002/01.dcm",
      "path/to/series002/02.dcm",
      "path/to/series002/03.dcm"
    ]
  }
]
```

{% embed url="https://www.loom.com/share/5c8b1ee72d8246b4a41a1af26757164a" %}
Example of a single series task on RedBrick AI
{% endembed %}

### Multi-Series Task

To perform Study level annotations, you can create a single task with multiple series. The following [items list](../importing-data/import-cloud-data/creating-an-items-list.md#items-list-format) structure will create **two tasks on RedBrick AI**, each with **2 series**.&#x20;

```json
[
  {
    "items": ["path/to/study01/series001.nii", "path/to/study01/series002.nii"]
  },
  {
    "items": [
      "path/to/study02/series001/01.dcm",
      "path/to/study02/series001/02.dcm",
      "path/to/study02/series001/03.dcm",
      "path/to/study02/series002/01.dcm",
      "path/to/study02/series002/02.dcm",
      "path/to/study02/series002/03.dcm"
    ]
  }
]
```

{% embed url="https://www.loom.com/share/ba982d0e9af748518a6e040b1f5f9bd5" %}
Example of a multi-series task with 4 series per task
{% endembed %}
