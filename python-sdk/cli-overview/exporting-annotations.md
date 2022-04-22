# Exporting Annotations

The CLI is a developer friendly way of exporting your annotations and data. Before getting started with this guide, make sure you have set up the [credentials for the CLI.](./#create-a-credentials-config)

{% embed url="https://www.loom.com/share/a7b5de48a16b4131b44c9911aee077d8" %}
Overview of RedBrick AI CLI Export
{% endembed %}

## Clone a Project

Much like Git, the first operation you need to do before exporting data is clone an existing project you have. Follow this guide to see [how to clone a project](exporting-annotations.md#clone-a-project).&#x20;

## Export Data from your Project

The CLI will only fetch the newly created annotations in your project and update your cloned project folder.&#x20;

For e.g. if you upload 10,000 images in your project, and annotate 8,000 images then export using the CLI, the CLI will export 8,000 tasks. A day later if you annotate another 5, the CLI will update the exported data with the 5 new tasks.

To export your data, you need to first go to your project directory

```
cd Project-1
```

To export the latest state of all your tasks (even the ones queued in labeling and review stages) run the following command.&#x20;

{% hint style="info" %}
This will only download newly created annotations; therefore, running this command with no changes to your project will export 0 tasks.&#x20;
{% endhint %}

```
redbrick export
```

If you want to fetch only the tasks in the ground truth stage, you need to run the following command.

```
redbrick export groundtruth
```

To clear the local redbrick cache and force download all the annotations again, run the following command.&#x20;

```
redbrick export --clear-cache
```

### Exporting segmentations in NifTI-1

To export DICOM project labels in [NIfTI-1](https://nifti.nimh.nih.gov/nifti-1/) format, run the following command.

```
redbrick export --format nifti
```

Doing so will export labels in `nifti` directory inside the project directory.

```
tree .
.
└── nifti
```

Please view the [format reference](exporting-annotations.md#exporting-segmentations-in-nifti-1) for a detailed description of the export format.&#x20;

### Export annotations with image files

To export your annotations along with the raw data files, run the following command.

```
redbrick export --with-files
```

Doing so will export tasks in `images` / `videos` / `dicom` directory (based on project type) inside the project directory.

