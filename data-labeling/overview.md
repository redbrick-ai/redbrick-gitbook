# Overview

The RedBrick AI platform offers several manual and automated tools for image and video labeling. The table below covers the current offerings of the platform:

| Data Type | Label Type |
| :--- | :--- |
| `Image` | Bounding Box |
|  | Segmentation |
|  | Polygon |
|  | Keypoint |
|  | Ellipse |
|  | Classification |
| `Video` | Bounding Box |
|  | Polygon |
|  | Classification |

## Labeling Interface Layout

The labeling interface is simple and easy to get started with. The figure below will help you get acquainted with the labeling tool interface. 

![Labeling interface layout](../.gitbook/assets/label-page.svg)

### Side Bar

![Example Side Bar \(image labeling\)](../.gitbook/assets/app.redbrickai.com_f5924ece-e355-48d2-8f9d-064c3440cef3_projects_287c2e7b-2c57-4489-8e0e-e332826ea940_tool_label_taskid-e575a0a1-7a18-4162-91d5-1a44b370fe3c-2x.png)

The sidebar contains all the relevant information for adding, and modifying labels. The **current label** sections displays a list of all the classes in your taxonomy for you to label. When a created label is selected, its class will be highlighted in this list. The **all labels** sections contains a list of all the created labels. The **label actions** section contains buttons for actions like removing labels, tracking labels in videos etc.

### **Top Bar**

![Sample Topbar \(manual-labeling\)](../.gitbook/assets/app.redbrickai.com_f5924ece-e355-48d2-8f9d-064c3440cef3_projects_287c2e7b-2c57-4489-8e0e-e332826ea940_tool_label_taskid-e575a0a1-7a18-4162-91d5-1a44b370fe3c-1-2x.png)

The top bar contains high level actions like submitting/saving tasks and accepting/reviewing tasks during quality assurance. Furthermore, the top bar contains high level information about each task - like: 

* **The data point name**: the file path, or the url of the task \(same as the [items list entry](../data-warehouse-1/preparing-your-data.md#prepare-your-items-list)\)
* **Timer**: the amount of time you have spent on this particular data point. This information is stored and provided to admins. 



### **Tool Bar**

![Sample Tool Bar for multi label type image labeling](../.gitbook/assets/app.redbrickai.com_f5924ece-e355-48d2-8f9d-064c3440cef3_projects_287c2e7b-2c57-4489-8e0e-e332826ea940_tool_label_taskid-e575a0a1-7a18-4162-91d5-1a44b370fe3c-2-2x.png)

The tool bar contains useful tools labeling actions, and tools specific to the label type you are working with. Some of the generic functions are:

* **Zoom:** zoom in and zoom out.
* **Selection tool:** disables editing on the interface. 
* **Visualization controls:** allow you to change the brightness, and contrast of the image as well as the opacity of the labels.

The tool bar also lets you choose what labeling tool you want to use if you have created your project with the _multi label type option_. 

### **Labeling Canvas**

The labeling canvas is where you will interact with the data and labels and actually add, edit, remove labels to data. Depending on the type of labels you are generating, the actions required to create/edit the labels will change. 

## Keyboard and Mouse Shortcuts 

| Mac | Windows | Description |
| :--- | :--- | :--- |
| ⌘C | Ctrl + C | Copy a label |
| ⌘V | Ctrl + V | Paste a label |
| ⌘Z | Ctrl + Z | Undo an action |
| ⌘⇧Z | Ctrl + Shift + Z | Redo an action |
| Mouse scroll | Mouse Scroll | Zoom in/out |
| esc | esc | De-select a selected label |
| w | w | Increase segmentation brush size |
| s | s | Decrease segmentation brush size |
| a | a | Previous frame in video |
| d | d | Next frame in video |

