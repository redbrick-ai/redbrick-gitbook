# Annotation Format NIfTI

## Export Folder Structure

RedBrick AI exports Medical Segmentations in the [NIfTI-1](https://nifti.nimh.nih.gov/nifti-1/) format. When you export your annotations, you will receive the NIfTI annotations and an [image/annotation items map](annotation-format-nifti.md#items-json).

Your exported annotation files will be in a directory named after your `project_id`, with the following structure:

```
project_id/
├── nifti
│   ├── <taskid>.nii
│   └── <taskid>.nii
└── tasks.json
```

Each exported NIfTI file will be assigned a unique `task_id` as its name. RedBrick AI assigns each of your tasks a unique Task ID that can be used to identify the task (for e.g. you can search by Task ID on the Data Page).&#x20;

The `tasks.json` will contain important information that will help you map between your annotations and images, and the JSON file will contain information about your instance ID's and category name's.&#x20;

## Items JSON

The image/annotation map file contains information about your annotations, images, and class categories. This file format is the same for uploading annotations and exporting annotations.

There will be a **single entry for each task** in the items file. Please see the definition of the JSON object below:

```typescript
type Items = Task[]
type Task =  {
  items: String;
  name?: String;
  segmentations: String[] | String[][];
  segmentMap?: { [key: number]: String };

  // Present in export, not required on upload
  taskId?: String;
}

```

#### `items: String`

The items entry is a list of file paths that point to your data. Please have a look at the[#items-list-format](../../importing-data/configuring-external-storage/#items-list-format "mention")to understand how to format this array for various modalities and series/study uploads.

#### `name: String`

A user defined unique string that is defined on upload, the exported file will include this value. The `name` is meant to be a human readable string that can help you identify tasks e.g. you can set the `name` of your series tasks to `patient01/study01/series01`.

#### `segmentations: String[] | String[][]`

The `segmentations` includes references to your semantic/instance segmentation NIfTI files.&#x20;

* **Series Task (`segmentations: String[]`)**\
  ****If your task is a series task i.e. the list of files in the `items` entry correspond to a single series, segmentations can be a single NIfTI file containing semantic segmentation labels or multiple NIfTI files containing instance segmentations for that series. For example -&#x20;
  * `segmentations: [series01_seg.nii]` (single annotation file for the series)
  * `segmentations: [series01-category01_seg.nii, series01-category02_seg.nii]` (multiple annotation files for the series).&#x20;
* **Study Task (`segmentations: String[][]`)**\
  ****If your task is a study task i.e. the list of files in `items` corresponds to multiple series, your segmentation files will be a nested list of file paths with each entry containing the file(s) for a single series in your study. For example -&#x20;
  * `segmentations: [[study1/series1_seg.nii], [study1/series2_seg.nii]]` (annotation files for two series in a single study)
  * `segmentations: [[study1/series1-category1_seg.nii, study1/series1-category2_seg], [study2/series1-category1_seg.nii]]` (annotation files for two series in study1, and 1 series in study2).

#### `segmentMap: {[key: number]: String}`

The `segmentMap` entry provides a mapping between the NIfTI class ID/instance ID and the RedBrick AI Taxonomy category name. If you are working with semantic segmentation labels, the `segmentMap` entry will be the same for all tasks.&#x20;

#### `taskId: String`

A RedBrick AI generated unique string for each task.
