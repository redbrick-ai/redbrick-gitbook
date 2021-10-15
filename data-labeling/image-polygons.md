# Image Labeling

{% hint style="info" %}
We have only included guides for the more complicated label and data types. Several tools - like image bounding box, and image key points are straightforward and intuitive to use and will be easy to get started with!
{% endhint %}

## Image polygons

The image polygon tools allow you to annotate and edit images with polygons. Polygons are closed shapes with an arbitrary number of vertices that are joined by edges. You can perform the following actions in the polygon labeling interface:

**Create a polygon**

Click on the labeling interface to add a vertex of a polygon, alternatively, you can click hold and drag to drop several vertices on the interface. Once you have added all the vertices to the interface, and want to complete the label, simply **double click**_ _to close the polygon. 

**Add a vertex**

To add a vertex to a polygon label that has already been created, select the label, and **double click** on the edge where you wish to add a node. A new node will be added to the center of this edge. 

**Delete a vertex**

To delete a vertex of a polygon that has already been created, **drag** the vertex that you wish to delete on to a neighboring vertex. You will see the vertex expand, at which point you can release and the vertex will be deleted. 

## Image Segmentation

The image segmentation tools allow you to annotate images with pixel level labels. The interface offers a circular, and square brush with adjustable sizes to create pixel level segmentation labels. 

**Creating a new instance**

Create a new segmentation label by selecting a label class and 'painting' on the labeling canvas - this will draw the pixel segmentation on the canvas. To create the instance, simply press `esc`.

**Editing an existing instance**

To edit an existing segmentation instance, select the label from the sidebar and make any edits that you wish - changing the shape, label class etc. Once you are happy with your edits, press `esc` to finish the edit. 
