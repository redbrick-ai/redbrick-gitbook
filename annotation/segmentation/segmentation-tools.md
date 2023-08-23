# Segmentation Tools

{% embed url="https://www.loom.com/share/c0986dc6a4274bffaa52031c98b24930" %}
Overview of all the segmentation tools
{% endembed %}

## Brush Tool

The Brush Tool has two modes - 2D and 3D (toggled on the right-side panel). The 2D brush is a circle, and the 3D brush is a sphere that segments across slices. You can adjust the size of the brush using the slider on the right-side panel, or the `w` & `s` hotkeys.&#x20;

{% hint style="info" %}
`Left click + drag` to segment and `right click + drag` to erase.
{% endhint %}

## Pen Tool

The Pen Tool has two modes - 2D and 3D (toggled on the right-side panel). The Pen Tool allows you to annotate using a free-form contour. In 3D mode, the free-form contour is extruded above and below the current slice.&#x20;

{% hint style="info" %}
`Left click + drag` to add a segment region and `Left click + drag` to remove a region.
{% endhint %}

## Region Growing

Region growing is a semi-automated segmentation tool that uses image intensity information to segment regions. By clicking and holding in a region, the segmentation will grow outward from the seed point (where you clicked). The longer you hold, the longer the region will grow.&#x20;

{% hint style="info" %}
`Right click + hold` to segment, `left click + hold` to erase.
{% endhint %}

## Contour Tool

The Contour Tool allows you to draw outlines of your regions quickly and then interpolate between slices.

To activate it - (a) select the tool from the top bar, (b) press the "k" hotkey, or (c) search for the Contour Tool in the command bar.

#### Creating a contour & interpolating

1. To get started, click on a 2D viewport. You can click and drag or add points one click at a time.
2. To close/complete the contour, click the end node.&#x20;
3. You can then change the slice and repeat the process. If you skip slices, **the in-between slices will be interpolated.**

#### **Editing a contour**

To edit, hover near the edge of your region and click and drag to draw a new segment. Editing an interpolated contour will automatically adjust the neighboring interpolated contours.

#### Rasterize to complete the contour

{% hint style="warning" %}
When you finish your contour, you must convert it to a pixel mask. This process is called "rasterization." There is a button on the right panel to do this, or you can use the `Shift+Enter` hotkey.
{% endhint %}

#### Smart Contouring

Our Smart Contour Tool automatically draws a contour around a region of interest. To use it, while the Contour Tool is selected, press `ctrl+alt/option` and hover near the boundary of an object. Click to confirm the automatic contour.&#x20;

For bumpy boundaries, you can attempt to smooth out the contour by holding and dragging, adjust the distance you drag to make the contour less or more smooth.

{% embed url="https://www.loom.com/share/63a8f0e45b934b2ab4d9cb3127e4c6b1" %}

{% hint style="warning" %}
In the video above, the hotkey is referenced as "Command or Control" but the correct key is `ctrl+alt/option`
{% endhint %}

## Hole Filling&#x20;

The Hole Filling Tool iteratively fills small holes in your Segmentation. Click anywhere on the canvas to start filling the small holes.

{% hint style="info" %}
Hole filling is designed to fill _small holes_. For larger holes, you may need to run it more than once to close the hole completely.&#x20;
{% endhint %}

{% hint style="warning" %}
For large volumes, 3D hole filling can be very computationally expensive. If your data has more than 800 slices, we recommend only using 2D hole filling.
{% endhint %}

## Paint Bucket

The Paint Bucket is helpful for closing single large holes. With the paint bucket tool selected, click in any large hole to fill it automatically.&#x20;

## Island Removal

Island Removal deletes islands of segmentations. Simply click on any "island" segmentation to remove it. On the right side context panel, you can enable "keep currently selected" to remove all islands except the one you clicked on.

## Merge Tool

The Merge Tool allows you to transform one type of segmentation island into another through a "merging" process. With Segmentation X selected, enable the Merge Tool and click on an island of Segmentation Y to merge the island to Segmentation X.&#x20;

## Thresholding

Thresholding allows you to _bound_ the intensity values in your image that will get segmented. Thresholding can be combined with any of the tools above to allow for faster segmentation.&#x20;

To activate thresholding, select the threshold filter from the top bar and select the threshold region from the right sidebar slider. You can also interactively select the threshold region by toggling the **Threshold Range Selector**, then left-click on the canvas to add a region and right-click on the canvas to remove it.&#x20;

{% hint style="info" %}
As long as the threshold filter is active, i.e. highlighted on the top bar and present on the right panel, the volume will remain thresholded.&#x20;

If you find the preview to be distracting, you can disable it in the right hand sidebar.&#x20;
{% endhint %}

## Fast Automated Segmentation Tool (F.A.S.T. ⚡️)

{% embed url="https://www.loom.com/share/285e0936b10e4f3eb26e6917b94e7d93" %}

The Fast Automated Segmentation Tool (F.A.S.T.) is an automatic segmentation tool powered by Meta AI's Segment Anything Model that allows users to rapidly generate 2D and 3D segmentations.&#x20;

F.A.S.T. is powerful because of the way users can prompt the tool to generate an accurate segmentation in real time. Under the hood, there are two components to the system:

1. **Image encoding**, which takes place on the server side. The result of image encoding is _embeddings_, which are special vector representations of the images that are useful for machine learning.
2. **Segmentation decoding**, which takes place in the browser in real time.

{% hint style="info" %}
**To enable F.A.S.T. for your Organization**, please do the following:&#x20;

1. Request access at https://redbrickai.com/fast.
2. Add the following code snippet to the _Hanging Protocols_ script in your Project Settings. [See this video here](https://www.loom.com/share/60f5bf88d9b44a98a2183df748ac8e22)**.**
{% endhint %}

{% code lineNumbers="true" %}
```javascript
setSegmentationSettings([{
    toolName: 'FAST',
    enabled: true,
}])
```
{% endcode %}

### Generating 2D Segmentations with F.A.S.T.

To start segmenting, create a segmentation instance, select the F.A.S.T. tool from the top bar or using `cmd/ctrl + b`. Once the tool is selected, hover over a viewport to start embedding computation for a single slice (you will see a loader spinner on the top right of the viewport). You can prompt F.A.S.T. in a few different ways after the embedding computation is complete:&#x20;

1. **Bounding Box prompts.** `Click + move mouse + click` to draw a bounding box. You will see the segmentation prediction compute in real time while you draw the bounding box.&#x20;
   1. **Key point refinement.** After you draw the bounding box, you can optionally refine the segmentation by prompting the system with key points. `Left click` to add regions you want to _add to the segmentation._ `Right click` to remove regions from the segmentation prediction.
   2. Once you are happy with the segmentation preview, confirm it by using the button on the right panel or `shift + enter`.
2. **Instant click.** `alt/option + hover` over objects to view a prediction preview. If you are satisfied with any preview, click while pressing `alt/option` to confirm the segmentation.&#x20;

### Generating 3D Segmentations with F.A.S.T.

3D F.A.S.T. allows users to draw Bounding Boxes to define an interpolation range for a 3D structure that is to be annotated.

The process for creating annotations with 3D F.A.S.T. is extremely similar to that of [2D F.A.S.T.](segmentation-tools.md#generating-2d-segmentations-with-f.a.s.t.) You can find a full step-by-step breakdown of how to use 3D F.A.S.T. below.

1\. Create a new Instance of your desired Object Label by clicking on the “+” in the left hand toolbar;

2\. Select F.A.S.T. in the top of the screen and wait for the embedding computation to complete on Slice X;

3\. Create a Bounding Box around the structure you wish to annotate;

4\. (Optional) Provide F.A.S.T. with additional input by using LMB/RMB;

5\. Navigate to the end of the range that you want to interpolate across (i.e., Slice Y);

6\. Repeat Step 3 (and optionally, Step 4) for the structure you wish to annotate on Slice Y;

7\. Once you are satisfied with the annotations, press Enter or click on “Finalize” in the right hand toolbar to generate the pixel masks on every slice between Slice X and Slice Y.

{% hint style="info" %}
Processing times may increase when interpolating across large ranges. However, please note that all subsequent work across the same range should be much faster, as the embedding computations only have to be computed once per slice.
{% endhint %}

{% hint style="danger" %}
Firewalls, ad blockers, privacy extensions, and any other browser extensions that block HTTP traffic are known to interfere with FAST.
{% endhint %}

## Linear Pixel Interpolation

In order to toggle linear pixel interpolation while annotating, click on the Command Bar (or use `CMD/CTRL+K`) and select "Toggle linear pixel interpolation".

<figure><img src="../../.gitbook/assets/linear-pixel-interpolation.gif" alt=""><figcaption></figcaption></figure>

## Tool Configuration

Your labeler toolkit can be customized at the Project level by navigating to the **Tool Settings** page within your Project Settings.

Simply utilize the checkboxes for each tool to:

* set a custom default tool;
* restrict/enable 2D and/or 3D annotation;
* set a default mode (i.e. 2D or 3D);
* enable/disable a Tool entirely;

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-23 at 3.44.13 PM.png" alt=""><figcaption></figcaption></figure>
