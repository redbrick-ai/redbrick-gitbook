# Direct data upload

## DICOM Projects

We support `.dcm`, `.dnii` and `.nii.gz` file uploads within DICOM projects.&#x20;

### DCM upload

When upload `.dcm` files, we require folder uploads with each folder containing the `.dcm` files for a single study. RedBrick will assume all the `.dcm` files within a _single_ root folder are part of a single study, and will form 1 task.&#x20;

{% embed url="https://www.loom.com/share/0d165117cd924c91b8fd9ed0f5112fd9" %}

### NIfTI Upload

You can upload `.nii` and `.nii.gz` files directly to RedBrick AI.

## Video Projects

For video projects you can upload MP4 files and we will handle the parsing down to frames. Videos will be split into frames at the full frame rate of the videos. Any frames beyond the first 5000 will be removed. It is strongly recommended to keep video clips shorter to assist annotators. Each video uploaded will be made into an individual task.

## Image

This is a simple process of just uploading the files that you want to use to create tasks. Each file will be made into a task that can be used further in your project pipeline. The task will have its name set by default to the file name. RedBrick AI supports `.png` `.jpeg` `.jpg` `.bmp`
