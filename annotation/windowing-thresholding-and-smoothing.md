# Windowing, Thresholding, and Smoothing

To help with visualizing your volumes and performing annotations, you can apply several filters to your volumes. The filters are available on the left side of the top bar - they are the first set of tools displayed.&#x20;

Please see the video below for a comprehensive overview of all filters - Windowing, Thresholding, and Smoothing.

{% embed url="https://www.loom.com/share/da10d5c39a3c4a46bc9e3e510f5a8200" %}
Filters
{% endembed %}

{% hint style="info" %}
The Smoothing function can now be found within the Command Bar or by using the `SHIFT+S` hotkey.
{% endhint %}

## Windowing

You can window your volumes by pressing `CTRL` and `LEFT CLICK` dragging on any viewport - up/down to adjust window level, left/right to adjust window width.&#x20;

{% embed url="https://www.loom.com/share/17f871afe6f747ae8124bfde408e2526?sid=ca2b398b-c97f-4c52-b280-8d8efec20a42" %}
Configuring Windowing Settings
{% endembed %}

You see and/or modify the current window settings by selecting the Windowing Tool on the top left of the tool bar. When the Windowing Tool is selected, its **settings will display in the right hand Context Panel.**

## Thresholding

To speed up segmentation, you can create a thresholding range by applying an upper and lower boundary for the HU values/intensities of your image or volume. With Thresholding enabled, you will only be able to create annotations within the thresholding range that you set, making it easy to avoid painting "outside the lines" of your target structure.

{% embed url="https://www.loom.com/share/07bc7a777db14b54b452da2a29f3d031?sid=17cf9d2e-ec2b-48bc-b7ff-c993d1b4aa65" %}
Configuring Thresholding Settings
{% endembed %}

To enable Thresholding, select the Threshold Panel in the top bar. You can manually adjust the threshold bounds using the slider/input fields.&#x20;

You can also use the **Threshold Range Selector, which allows you to interactively select the bounds** - with the Range selector Toggled, `left click` any part of a viewport to include it in the threshold range, `right click` to exclude it. &#x20;

{% hint style="warning" %}
The threshold will be applied as long as the threshold filter is toggled - the settings are visible in the right hand Context Panel.
{% endhint %}

{% hint style="info" %}
Toggle the Preview in the Threshold Context Panel to visualize your thresholded region.
{% endhint %}

## Smoothing

You can smooth your volumes to remove noise from the data and simplify segmentation tasks. Smoothing works well when used alongside thresholding or other [Segmentation Tools](segmentation/segmentation-and-other-tools.md) such as [Region Growing](segmentation/segmentation-and-other-tools.md#region-growing).&#x20;

You can activate smoothing with the following steps or using the `SHIFT+S` hotkey:

1. Open the Command Bar by clicking the icon in the bottom right hand corner or using `CMD/CTRL+K`;
2. Enter "toggle image smoothing" into the search field;
3. Click on "Toggle image smoothing" when it appears;

{% hint style="warning" %}
For large volumes, smoothing can take up to several minutes to compute and apply!
{% endhint %}
