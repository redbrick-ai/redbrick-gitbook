# CLI Overview

The RedBrick CLI is a tool to interact programmatically with the RedBrick AI platform. The CLI provides a developer friendly way to perform important functions like export, project creation etc.&#x20;

{% hint style="info" %}
The RedBrick SDK works on Mac, windows, and linux, and is available on [pypi](https://pypi.org/project/redbrick-sdk/). The SDK is compatible with **3.70 <= Python < 3.10**
{% endhint %}

{% hint style="info" %}
The CLI is included along with the Python SDK _after version 0.7.0._
{% endhint %}

## **Generate an API Key**

You can create an API key for your organization under _Organization Settings_, which is accessible by clicking on the bottom left corner of the screen.

## Install the CLI

The CLI can be installed from pypy.

```bash
pip install redbrick-sdk
```

## Create a credentials config

To easily manage authentication so that you can interact with your RedBrick AI account, you will have to create a credentials config which will be stored on your system.&#x20;

```bash
redbrick config
> Org ID: TODO
> API KEY: TODO
> URL: TODO
> Profile name: TODO
✔ RedBrick AI Organization
```

Retrieve your organization ID from project settings, or the application URL - https://app.redbrickai.com/\<org\_id>/. Your credentials will be saved at `~/.redbrick/credentials` using the profile name specified.&#x20;

## Clone an existing project

To export your data from your project, you have to first clone it.&#x20;

You can do this by selecting from the list of projects.

```
redbrick clone
>   Project-1 (project_1_id)
    Project-2 (project_2_id)
```

You can also directly specify the `project_id` of your project (found in project settings, or https://app.redbrickai.com/\<orgid>/\<projectid>).&#x20;

```
redbrick clone project_1_id
```

Doing so will create a project folder in your existing directory.&#x20;

```
tree .
.
└── Project-1
```

## Export data from your project

The CLI provides a git like interface for exporting data from your projects. The CLI will only fetch the newly created annotations in your project and update your cloned project folder.&#x20;

For e.g. if you upload 10,000 images in your project, and annotate 8,000 images then export using the CLI, the CLI will export 8,000 tasks. A day later if you annotate another 5, the CLI will update the exported data with the 5 new tasks.

To export your data, you need to first go to your project directory

```
cd Project-1
```

To export the latest state of all your tasks (even the ones queued in labeling and review stages) run the following command. Note - this will only download newly created annotations; therefore, running this command with no changes to your project will export 0 tasks.&#x20;

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
