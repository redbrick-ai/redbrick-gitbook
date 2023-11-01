# Overview

The RedBrick AI DICOM Annotation Tool is a web-based annotation tool with native support for DICOM medical images. The solution supports 2D and 3D data and allows for segmentation, classification, and vector annotations.&#x20;

## Interface Overview

![](<../.gitbook/assets/Group 28384.png>)

There are 4 main components to the annotation interface:

1. Left Sidebar: this is where you create, edit and interact with annotations and attributes
2. Top Bar: the top bar contains Task-level actions such as task submission and saving, as well as the Thresholding, Windowing, and Segmentation Tools
3. Context Panel: shows additional information and settings for any **currently** **selected** tool(s)
4. Main Canvas: where you interact with your images and apply your annotations to your images/volumes

## Navigating your Volume

If you've used other DICOM viewers, you may already be familiar with the commands necessary for navigating volumes on RedBrick AI.

* **Changing slices:** change slices by scrolling on any of the viewports. You can also use the slider on the left side of each view port to move through the volume quickly. Using the `up arrow`  and `down arrow`  keys will change one slice at a time on the selected viewport. You can also hold `alt/option` and drag to quickly scroll across slices
* **Zoom:** zoom into your volume by holding `ctrl + scroll` on Mac, or `shift + scroll` on Windows
* **Pan:** pan around your volume with `shift + left click drag`
* **Crosshairs:** synchronize re-constructions of the same Series by enabling the Crosshair Tool in the Top Bar. This feature is only available when you have 3 orthogonal reconstructed views (Sagittal, Coronal, and Axial)
* **Reset:** reset all views to their default state (i.e. center slice and neutral zoom) with `space`
* **3D view:** a 3D view of your image can be enabled on the bottom right of the 3D viewport. Once enabled, you can interact with your 3D volume using the following actions:
  * **Rotate** the volume with`left click` + `drag`
  * **Zoom** into your volume with`scroll`
  * **Pan** across your volume with`shift` + `left click` + `drag`
  * **Rotate** the volume **in the plane** with `ctrl` + `left click` + `drag`
* **Windowing:** modify the window width and level by holding `ctrl + left click drag`
* **Min / Max viewport:**  with a 2x2, 2x3, or 3x2 layout configuration, toggle min/max by pressing `enter` or `return`
* **Change selected viewport:** the selected viewport (i.e. the viewport that you last clicked in) can be quickly changed by using `shift + arrow keys`. This hotkey can be combined with min/max to quickly explore your views.

## How Tasks Work with DICOM Annotation

On RedBrick AI, a Task is a single unit that moves through the annotation workflow. A single Task is served to Labelers/Reviewers to complete in one session.&#x20;

Typically, there will be a 1-1 mapping between a **DICOM series** and a RedBrick AI Task. If you have 1,000 Series, the typical use case would be creating 1,000 Tasks in the RedBrick AI annotation workflow.&#x20;

Alternatively, you can choose to create a multi-series Task, or a Task that has 1-1 mapping between a **DICOM study** and a RedBrick AI Task.&#x20;

### Single Series Task

When uploading your [Items List](../importing-data/import-cloud-data/creating-an-items-list.md), this is the structure to follow for creating a single-series Task (i.e. only one Series per items entry).&#x20;

The following structure will create **two tasks on RedBrick AI**, with each task having a **single series only**.&#x20;

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

To perform Study-Level annotations, you can create a single Task with multiple series. The following [Items List](../importing-data/import-cloud-data/creating-an-items-list.md#items-list-format) structure will create **two Tasks on RedBrick AI**, each with **2 series**.&#x20;

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
Example of a multi-series task with 4 series per Task
{% endembed %}

### Task-Level and Series-Level Metadata

RedBrick supports the creation of Task-Level and Series-Level metadata when uploading Tasks via the Python SDK.

{% hint style="info" %}
With the [current version of the Python SDK](https://pypi.org/project/redbrick-sdk/#history) (2.12), metadata can only be created upon Task upload via SDK.&#x20;
{% endhint %}

**Metadata cannot be modified or deleted in any way after Task upload,** although these features are in our Product Roadmap for the future. If you'd like to alter or delete metadata from a Task that has already been uploaded, you should delete the original Task and upload it again.

To add metadata to a Task or Series, simply add the `metaData: {}` object when [importing data (or annotations)](https://docs.redbrickai.com/python-sdk/sdk-overview/importing-data-and-annotations). All information in `metaData: {}` will be stored as strings within a key-value pair, and any strings that contain **only links** will be converted to clickable links within the Annotation Tool.

Please see the example code below, which adds the Task and Series-Level metadata to the `points` object (which is commonly used when uploading data):

```python
points = [
            {
            "name": "Task Name",
            "metaData": 
                {
                    "Name": "Task Metadata",
                    "Link": "https://www.examplelink.com"
                },
            "series": 
                [
                    {
                        "name": "Series Name",
                        "items": [],
                        "metaData": {
                                "Name": "Series-Level Metadata"
                        },
                    },
                ],
            },
        ]
```

After a successful upload, your metadata will be visible within the Editor in the bottom-left corner of each viewport. You can also click on **View Metadata** to expand a dialog box containing a more comprehensive view of your metadata.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-05 at 11.38.54 AM.png" alt=""><figcaption><p>The Metadata dialog box, expanded</p></figcaption></figure>

All metadata assigned to a Task or Series will also be visible in the `tasks.json` file upon export.

{% hint style="warning" %}
Please note the following privacy-related information about how RedBrick AI handles Task and Series-Level Metadata:

* Task and Series-Level Metadata does not reference any information related to an image/volume's DICOM headers
* RedBrick AI automatically masks all information related to a Task and Series-Level Metadata&#x20;
{% endhint %}
