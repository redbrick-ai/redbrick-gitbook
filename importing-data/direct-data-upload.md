# Direct data upload

The Direct Upload functionality allows users to upload their image data directly to RedBrick AI servers. Direct Upload is commonly used for light experimentation with a small dataset.&#x20;

{% hint style="warning" %}
All image data directly uploaded will be stored on RedBrick AI servers. If you don't want RedBrick AI to host your image data, [please integrate your storage](import-cloud-data.md).
{% endhint %}

RedBrick AI supports a variety of different image formats:&#x20;

1. DICOM - .dcm, .ima, .dicom, .dicm
2. NIfTI - .nii, .nii.gz
3. Videos - .mp4, .mov, .avi
4. RGB Images - .png, .jpeg, .jpg, .bmp

Navigate to the project you want to upload data within to upload your scans. Click on "Upload Data" on the top-right of the dashboard.&#x20;

1. Select the type of data you want to upload. \
   Note - you **can only upload one type of image data** (DICOM, NIfTI, etc.) at one time, and each data type **has its folder structure format**.
2. For DICOM & NIfTI volume data, select yes/no for _group by study_. Grouping by study allows you to upload multiple scans as a single task. This is useful when you want to [view/annotate multiple images (a full study) at once](https://docs.redbrickai.com/annotation/overview#how-tasks-work-with-dicom-annotation).&#x20;

## Folder Structure

### DICOM 3D Volume

Put all instances of a DICOM series in a folder. If you are uploading only 1 series, you can upload all the instances, not in a folder.&#x20;

<figure><img src="../.gitbook/assets/Label evaluation.png" alt=""><figcaption></figcaption></figure>

### NIfTI 3D Volume

Individual NIfTI files are uploaded as separate tasks. If you want to group tasks by study, put the NIfTI files of a single task/study in a folder.&#x20;

<figure><img src="../.gitbook/assets/Label evaluation (6).png" alt=""><figcaption></figcaption></figure>

### Image 2D

Individual 2D images are all uploaded as individual tasks. If you want to create a _study task_ with 2D images, please [use your external storage](import-cloud-data.md), or [upload data using the CLI](../python-sdk/cli-overview/importing-data/).

### Video Files

Individual 2D videos are all uploaded as individual tasks. If you want to create a _study task_ with 2D videos, please [use your external storage](import-cloud-data.md), or [upload data using the CLI](../python-sdk/cli-overview/importing-data/).

### Video Frames

Group all frames for a video in a single folder. The video frames will be naturally sorted using the frame filenames.&#x20;

<figure><img src="../.gitbook/assets/Label evaluation (5).png" alt=""><figcaption></figcaption></figure>
