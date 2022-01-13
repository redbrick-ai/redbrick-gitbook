---
description: >-
  A troubleshooting guide for making sure you are getting the best performance
  out of your computer and the RedBrick AI 3D DICOM annotation tool.
---

# Optimizing Performance

## Introduction

The RedBrick AI 3D DICOM tool is built into your browser using a common web technology called WebGL. Depending on your computer, your web browser, and the data you are labeling you may face performance problems. While we hope that you never experience any issues, this guide is here to help you optimize your computer to ensure you can get the best performance possible for your scenario.

### What is WebGL?

WebGL is a standard computing environment for graphics processing in a browser. This allows the browser to leverage your computers GPU to quickly render graphics much faster than if your CPU alone was being used.

## Factors that affect performance

There are ultimately three factors that will affect your performance: The power of your computer and GPU, the size of the rendering task, and the configuration of your browser and computer to make use of your GPU.

### Power of your computer and GPU

Similar to video games and video editing software, the maximum performance your computer can experience is limited by the power of your computer, specifically the GPU. Unfortunately, other than changing your computer there are no ways to improve this. At the end of this guide is a benchmark section where you can see some sample tests that have been run to know if your computer has enough power to complete your task.

### Size of the rendering task

The amount of work that is needed to renderer your reconstructed views will depend on the following 3 factors:

* **The size of the rendering window -** decreasing the size of your window you will decrease the amount of work needed to render the view.
* **The amount of data in the scan you are rendering -** this is a property of your data and cannot be modified.
* **Whether 3D reconstruction is enabled or disabled -**  by disabling the 3D reconstruction you can often improve performance.

### Configuration of your browser and computer to leverage your GPU

The most important factor that you have the most control over is making sure that your internet browser and your computer are correctly configured. Using GPUs can massively improve the performance of your computer on the task but sometimes special configuration is needed to enable this.

Some of the possible problem areas are:

* Are you using an updated version of your browser?
* Are OpenGL 2.0 or WebGL enabled on the browser?
* Is "hardware acceleration" enabled in the browser?
* If your computer has multiple graphics cards, is the highest performance one being used?

The rest of this guide will be trying to diagnose and address the above issues.



## Debugging

Tips, tricks, and guides to make sure you're getting the best performance you can get.&#x20;

### Quick ideas

Often times no configuration is needed to get the most out of your machine, but if you're having slow performance then these are some potential quick fixes you can try:

* Running the task in a different browser such as Google Chrome, Firefox, or Safari
* Updating your browser
* Closing other tabs and programs, especially those that might also require use of your GPU

### Diagnosing configuration problems

* Check that your browser supports WebGL [https://get.webgl.org/](https://get.webgl.org)
* Check your Task Manager (Windows) or Activity Monitor (Mac) for GPU usage while your DICOM rendering is slow. If the usage is not at 100%, then it is likely that your browser or computer is not using your GPU to speed up performance.

### Enabling Hardware Acceleration

When you use your GPU to perform WebGL rendering in your browser, this is called hardware acceleration. Different browsers, browser versions, and operating systems all have different default settings and options for enabling this. If your GPU usage is low but you are experiencing slow performance on the 3D DICOM tool, then you should try to enable hardware acceleration.&#x20;

You can check the following external guides for instructions on how to do this:

* Google Chrome: [https://www.lifewire.com/hardware-acceleration-in-chrome-4125122](https://www.lifewire.com/hardware-acceleration-in-chrome-4125122)
  * special emphasis should be given to enable the #ignore-gpu-blocklist flag
* Safari: [https://discussions.apple.com/thread/8655829](https://discussions.apple.com/thread/8655829)



{% hint style="info" %}
We will continue to update this guide over time with the most up to date information and techniques.

If you continue to have issues or this guide does not cover your setup, send us an email and we'll be happy to help make sure you are maximizing the performance for your unique situation.
{% endhint %}



