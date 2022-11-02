# Segmentation Tools

{% embed url="https://www.loom.com/share/c0986dc6a4274bffaa52031c98b24930" %}
Overview of all the segmentation tools
{% endembed %}

## Brush

The brush tool has two modes - 2D and 3D (toggled on the right side panel). The 2D brush is a circle, and 3D brush is a sphere that segments across slices. You can adjust the size of the brush using the slider on the right side panel, or the `w` & `s` hotkeys.&#x20;

{% hint style="info" %}
`Left click + drag` to segment and `right click + drag` to erase.
{% endhint %}

## Pen

The Pen tool has two modes - 2D and 3D (toggled on the right side panel). The pen tool allows you to annotate using a free-form contour. In 3D mode, the free-form contour is extruded above and below the current slice.&#x20;

{% hint style="info" %}
`Left click + drag` to add a segment region and `Left click + drag` to remove a region.
{% endhint %}

## Region Growing

Region growing is a semi-automated segmentation tool that uses image intensity information to segment regions. By clicking and holding in a region, the segmentation will grow outward from the seed point (where you clicked). The longer you hold, the longer the region will grow.&#x20;

{% hint style="info" %}
`Right click + hold` to segment, `left click + hold` to erase.
{% endhint %}

## Island Removal

Island removal removes islands of segmentations. Click on any "island" segmentation to remove it. On the right side context panel, you can active "keep currently selected" to remove all islands except the one you clicked on.

## Hole Filling&#x20;

Holde filling iteratively fills small holes in your segmentation. Click anywhere on the canvas to start filling the small holes.

{% hint style="info" %}
Hole filling is designed to fill _small holes_. For larger holes, you may need to run it more than once to close the hole completely.&#x20;
{% endhint %}

{% hint style="warning" %}
For large volumes, 3D hole filling can be very computationally expensive. If your data has more than 300 slices, we recommend only using 2D hole filling.
{% endhint %}

## Paint Bucket

Paint bucket is useful for closing single large holes. With the paint bucket tool selected, click in any large hole to automatically fill it.&#x20;

## Thresholding

Thresholding allows you to _bound_ the intensity values in your image that will actually get segmented. Thresholding can be combined with any of the tools above to allow for faster segmentation.&#x20;

To activate thresholding select the threshold filter from the top bar, and then select the threshold region from the right sidebar slider. You can also interactively select the threshold region by toggling "Threshold Range Selector", then left-click on the canvas to add a region, and right-click on the canvas to remove it.&#x20;

{% hint style="info" %}
As long as the threshold filter is active i.e. highlighted on the top bar and present on the right panel, the volume will remain thresholded.&#x20;

You can always disable the flashing preview, if it is distracting, from the right side bar.&#x20;
{% endhint %}
