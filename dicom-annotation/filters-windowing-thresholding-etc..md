# Filters - windowing, thresholding etc.

To help with visualizing your volumes and performing annotations, you can apply several _Filters_ to your volumes. The filters are available on the left side of the top bar - they are the first set of tools displayed.&#x20;

{% embed url="https://www.loom.com/share/da10d5c39a3c4a46bc9e3e510f5a8200" %}
Filters
{% endembed %}

## Windowing

You can window your volumes by pressing `CTRL` and `LEFT CLICK` dragging on any viewport - up/down to adjust window level, left/right to adjust window width.&#x20;

You see the current window settings/modify them by selecting the window tool on the top left of the tool bar. When windowing is selected, the **settings will be displayed in the context panel.**

## Thresholding

To speed up segmentation of your volumes, you can threshold a volume by setting an upper and lower bound on the intensities/HU values that will get segmented.&#x20;

To enable thresholding, select the threshold filter from the top bar. You can manually adjust the threshold bounds using the slider/input fields.&#x20;

You can also use **the range selector which allows you to interactively select the bounds** - with the range selector toggled, `left click` any part of a viewport to include it in the threshold range, `right click` to exclude it. &#x20;

{% hint style="warning" %}
The threshold will be applied as long as the threshold filter is toggled, and the settings are visible in the context panel.
{% endhint %}

{% hint style="info" %}
Toggle the preview in the threshold context panel to visualize your thresholded region.
{% endhint %}

## Smoothing

You can smooth your volumes to remove noise from the data and simplify segmentation tasks. Smoothing works well when used along side thresholding or other segmentation tools like region growing.&#x20;

Select the Smoothing filter from the top bar and enable/disable it from the context panel.&#x20;

{% hint style="warning" %}
1. For large volumes, smoothing can take up to several minutes to compute and apply
2. Smoothing will only be applied as long as the filter is selected on the top bar and the settings are visible in the context panel.
{% endhint %}
