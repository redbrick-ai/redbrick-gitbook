# Preview Tool

RedBrick AI's Preview Tool allows users to see how their images, volumes, and annotations are displayed within RedBrick AI's Annotation Tool without having to [create a Project](../quick-start/get-started-with-a-project.md#creating-a-project) or integrate a third-party [Storage Method](../importing-data/import-cloud-data.md).

As of `v1.2.3`., users can preview images and/or annotations from either their local machine or any Storage Method they have integrated into their RedBrick Organization.

***

### **Previewing a Local File**

1. Open the Preview Tool, located in the lefthand sidebar of the Home Page;
2. Select a file source: **Load from file system;**
3. Within **Preview Tool**, select the image(s) you would like to display or simply drag and drop them into the corresponding left hand window;
4. (Optional) select the annotation file you would like to display or simply drag and drop it into the corresponding right hand window;
5. Click on **View Data;**
6. Use the **Manage Files** button (top right hand corner) and **Replace** buttons (in the dialog menu) to swap out new files as needed;

<figure><img src="../.gitbook/assets/preview-tool.gif" alt=""><figcaption><p>Uploading a spine MRI scan and annotations to Preview Tool</p></figcaption></figure>

***

### Previewing a File on your Storage Method

Once you have opened the Preview Tool and selected Load from Storage Method:

1. Select a file source: **Load from Storage Method;**
2. In the **Select your external storage** dropdown, choose a Storage Method;
3. In the **List of items** field, provide the partial or full paths for the images you wish to preview, separated by a comma or newline;
4. Click on **View Data;**
5. Use the **Manage Files** button (top right hand corner) and **Replace** buttons (in the dialog menu) to swap out new files as needed;

***

### Other Functionality

Please note that images and volumes can be manipulated in Preview Tool just as they would be in the standard Annotation Tool. The following functions represent a non-exhaustive list of features available in Preview Tool:

* Windowing Settings
* Thresholding Settings
* MPR Layout
* Command Bar (and commands such as "toggle Linear Pixel Interpolation", "toggle permanent crosshairs", etc.)
* Oblique Planes
* Horizontal and Vertical Flipping
* Viewport Maximization and Minimization;
* ...and more!

***

### Notes on Annotation Files

1. If you are uploading a segmentation file that contains **non-segmentation annotations** (e.g. length measurements, bounding boxes, etc.), the non-segmentation annotations will **not** display in Preview Tool.
2. If you are uploading a segmentation file, Preview Tool will automatically map the annotations and display them as unique Instances in the left hand toolbar.
