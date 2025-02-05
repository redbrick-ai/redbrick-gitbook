---
description: >-
  This page provides an overview of RedBrick-compatible data formats for upload
  and export, as well as an overview of uploading data directly to RedBrick
  servers ("Direct Upload").
---

# Uploading Data to RedBrick

## Supported Image Import Formats

RedBrick AI supports a variety of different image formats:&#x20;

* NIfTI - .nii, .nii.gz
* DICOM - .dcm, .ima, .dicom, .dicm
* RGB Images - .png, .jpeg, .jpg, .bmp
* Videos - .mp4, .mov, .avi
* NRRD - .nrrd
* MHA - .mha
* MHD - .mhd in combination with a corresponding .raw or .img file

{% hint style="success" %}
You can see the list of supported image export formats [here](https://sdk.redbrickai.com/sdk.html#redbrick.export.Export.export_tasks).
{% endhint %}

Annotations on RedBrick are stored and exported in NIfTI format by default. However, RedBrick supports several other formats when uploading and exporting annotations.

### Supported Annotation Import Formats

* NIfTI - .nii, .nii.gz (default)
* RT STRUCT - .dcm
* MHD - .mhd

Further information can be found in our SDK reference [here](https://sdk.redbrickai.com/sdk.html#redbrick.upload.Upload.update_tasks_labels).

### Supported Annotation Export Formats

* NIfTI - .nii, .nii.gz (default)
* RT STRUCT - .dcm
* PNG - .png
* MHD - .mhd

Further information can be found in our SDK export reference [here](https://sdk.redbrickai.com/sdk.html#redbrick.export.Export.export_tasks).

{% hint style="success" %}
If you require additional support for a file format that is not present in this list, please reach out to us at support@redbrickai.com.&#x20;
{% endhint %}

## Direct Upload

The Direct Upload functionality allows users to upload their image data directly to RedBrick AI’s servers. We recommend using Direct Upload if you’re working with a small dataset or want to do some light experimentation with RedBrick’s toolset.

{% hint style="warning" %}
All image data that is directly uploaded to RedBrick AI’s servers will also be stored there. If you’d rather not have your image data hosted on our servers, we recommend [integrating your storage](import-cloud-data.md).
{% endhint %}

First, open a project that will serve as the destination for your upload. Then, click on **Upload Data** on the top-right of the dashboard.&#x20;

1. Select the type of data you want to upload. \
   \
   Please note that **you can only upload one type of image data** (DICOM, NIfTI, etc.) **at a time**, and **each data type has its own folder structure**.
2. With DICOM & NIfTI volume data, you can also choose to group your data by study. Selecting **Group by Study** allows you to upload multiple scans as a single task. This is useful [when you want to view or annotate multiple images (i.e. a full study) at once](https://docs.redbrickai.com/annotation/overview#how-tasks-work-with-dicom-annotation).&#x20;

## Folder Structure

### DICOM 3D Volume

Upload all instances of a DICOM series to a destination folder. If you’re only uploading a single series, you can do so without designating a folder.

<figure><img src="../.gitbook/assets/Label evaluation (8).png" alt=""><figcaption></figcaption></figure>

### NIfTI 3D Volume

Individual NIfTI files are uploaded as separate tasks. If you’d like to group your tasks by study, place all of the NIfTI files correlating to a specific task/study in a separate folder.

<figure><img src="../.gitbook/assets/Label evaluation (6).png" alt=""><figcaption></figcaption></figure>

### Image 2D

Individual 2D images are uploaded as individual tasks. If you’d like to create a study task with 2D images, please [use your external storage](import-cloud-data.md) or [upload data using the CLI](../python-sdk/cli-overview/).

### Video Files

Individual 2D videos are uploaded as individual tasks. If you’d like to create a study task with 2D videos, please [use your external storage](import-cloud-data.md) or [upload data using the CLI](../python-sdk/cli-overview/).

### Video Frames

All video frames in a folder are uploaded as a single task and sorted by file name.

<figure><img src="../.gitbook/assets/Label evaluation (5).png" alt=""><figcaption></figcaption></figure>
