# Preview Tool

RedBrick AI's Preview Tool allows users to see how their images, volumes, and annotations are displayed within RedBrick AI's Annotation Tool without having to [create a Project](../quick-start/get-started-with-a-project.md#creating-a-project) or integrate a third-party [Storage Method](import-cloud-data.md).

To visualize your data (and, optionally, your annotations) in Preview Tool:

1. Click on **Preview Tool** in the left hand toolbar of the **Home Page**;
2. Within **Preview Tool**, select the image(s) you would like to display or simply drag and drop them into the corresponding left hand window;
3. (Optional) select the annotation file you would like to display or simply drag and drop it into the corresponding right hand window;
4. Click on **View Data;**
5. Use the **Manage Files** button (top right hand corner) and **Replace** buttons (in the dialog menu) to swap out new files as needed;

<figure><img src="../.gitbook/assets/preview-tool.gif" alt=""><figcaption><p>Uploading a spine MRI scan and annotations to Preview Tool</p></figcaption></figure>

{% hint style="info" %}
If you are uploading a segmentation file, Preview Tool will automatically map the annotations and display them as unique Instances in the left hand toolbar.
{% endhint %}

Please note that images and volumes can be manipulated in Preview Tool just as they would be in the standard Annotation Tool. The following functions represent a non-exhaustive list of features available in Preview Tool:

* Windowing Settings
* Thresholding Settings
* MPR Layout
* Command Bar (and commands such as "toggle Linear Pixel Interpolation", "toggle permanent crosshairs", etc.)
* Oblique Planes
* Horizontal and Vertical Flipping
* Viewport Maximization and Minimization;
* ...and more!

{% hint style="warning" %}
If you are uploading a segmentation file that contains **non-segmentation annotations** (e.g. length measurements, bounding boxes, etc.), the non-segmentation annotations will **not** display in Preview Tool.
{% endhint %}
