# Direct Data Upload

The Direct Upload functionality allows users to upload their image data directly to RedBrick AI’s servers. We recommend using Direct Upload if you’re working with a small dataset or want to do some light experimentation with RedBrick’s toolset.

{% hint style="warning" %}
All image data that is directly uploaded to RedBrick AI’s servers will also be stored there. If you’d rather not have your image data hosted on our servers, we recommend [integrating your storage](import-cloud-data.md).
{% endhint %}

RedBrick AI supports a variety of different image formats:&#x20;

1. DICOM - .dcm, .ima, .dicom, .dicm
2. NIfTI - .nii, .nii.gz
3. Videos - .mp4, .mov, .avi
4. RGB Images - .png, .jpeg, .jpg, .bmp

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

Individual 2D images are uploaded as individual tasks. If you’d like to create a study task with 2D images, please [use your external storage](import-cloud-data.md) or [upload data using the CLI](broken-reference).

### Video Files

Individual 2D videos are uploaded as individual tasks. If you’d like to create a study task with 2D videos, please [use your external storage](import-cloud-data.md) or [upload data using the CLI](broken-reference).

### Video Frames

All video frames in a folder are uploaded as a single task and sorted by file name.

<figure><img src="../.gitbook/assets/Label evaluation (5).png" alt=""><figcaption></figcaption></figure>
