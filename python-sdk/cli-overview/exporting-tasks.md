# Exporting tasks

## Export annotations

You can export your projects annotations within [a local project directory](creating-and-cloning-projects.md). The CLI will fetch only the newly created annotations in your project.

For example, if you upload 10,000 images in your project, and annotate 8,000 images then export using the CLI, the CLI will export 8,000 tasks. A day later if you annotate another 5, the CLI will update the exported data with the 5 new tasks.

{% hint style="info" %}
Running this command with no changes to your project will export 0 tasks.&#x20;
{% endhint %}

{% hint style="success" %}
Please visit our [format reference](../reference/annotation-format.md) to see the format of the exported annotations.
{% endhint %}

To export your data, you need to first go to your [local project directory](creating-and-cloning-projects.md).

```bash
$ cd my-project
```

#### Export all tasks

To export the latest state of all your tasks (even the ones queued in labeling and review stages) run the following command.&#x20;

```bash
$ redbrick export
```

#### Export ground truth tasks only

If you want to fetch only the tasks in the ground truth stage, you need to run the following command.

<pre class="language-bash"><code class="lang-bash"><strong>$ redbrick export groundtruth
</strong></code></pre>

#### Export tasks and clear cache

To clear the local redbrick cache and force download all the annotations again, run the following command.&#x20;

```bash
$ redbrick export --clear-cache
```

#### Export tasks with images

If you want to download your images along with the created annotations, run the following command.&#x20;

```bash
$ redbrick export --with-images
```

In case you uploaded DICOM images, and want to export those images as NIfTI files (so that both your annotations and images are in the same format), run the following command.

```bash
$ redbrick export --with-images --dicom-to-nifti
```

#### Export tasks from a specific stage

If you want to export tasks that are queued in a specific stage, for example, exporting all tasks queued in Review\_2, you can do so in the following way:

```bash
$ redbrick export --stage Review_2
```

## Export an audit trail

Generating an audit trail can be useful material for regulators interested in your quality control processes and for managing your internal QA processes.&#x20;

You can create such a report by running the following command within your [local project directory](creating-and-cloning-projects.md).

```bash
$ redbrick report
```

The exported JSON object will contain data similar to what is shown below. Each entry will represent a single task (uniquely identified by `taskId`). The `events` array contains all key events/actions performed on the task, with `events[0]` being the first event.

```json
[
  {
    "taskId": "...",
    "currentStageName": "Label",
    "events": [
      {
        "eventType": "TASK_CREATED",
        "createdAt": "...",
        "isGroundTruth": false,
        "createdBy": "..."
      },
      {
        "eventType": "TASK_ASSIGNED",
        "createdAt": "...",
        "assignee": "...",
        "stage": "Label"
      }
    ]
  }
]
```
