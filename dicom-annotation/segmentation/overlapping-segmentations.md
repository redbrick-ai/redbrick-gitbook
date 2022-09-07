# Overlapping Segmentations

Typically in a single annotation task each voxel/pixel of an image gets only 1 classification e.g. background, tumor etc. However, **** sometimes you may want to annotate multiple overlapping structures and assign multiple classifications to the same group of pixels. On RedBrick AI you can accomplish this by creating an _**o**_**verlapping segmentation.**

Each segmentation tool e.g brush, pen, region growing etc. will have an **overlapping segmentation toggle in its context panel**. If you check the toggle, you will be able to create overlapping segmentation without overwriting existing annotations. When you export data with overlapping segmentations, all annotations will be exported as individual segmentation masks.&#x20;

Watch this video for an overview:

{% embed url="https://www.loom.com/share/5d22671b26674c8f9627bd6bc600db13" %}

****
