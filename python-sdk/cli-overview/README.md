# CLI Overview

The RedBrick CLI is a tool to interact programmatically with the RedBrick AI platform. The CLI provides a developer friendly way to perform important functions like export, project creation etc.&#x20;

{% hint style="info" %}
The RedBrick SDK works on Mac, windows, and linux, and is available on [pypi](https://pypi.org/project/redbrick-sdk/). The SDK is compatible with **3.70 <= Python < 3.10**
{% endhint %}

{% hint style="success" %}
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

To easily manage authentication to interact with your RedBrick AI account, you will have to create a credentials config that will be stored on your system.&#x20;

```bash
redbrick config
> Org ID: TODO
> API KEY: TODO
> URL: TODO
> Profile name: TODO
✔ RedBrick AI Organization
```

Retrieve your organization ID from project settings or the application URL - https://app.redbrickai.com/\<org\_id>/. Your credentials will be saved at `~/.redbrick/credentials` using the profile name specified.&#x20;

## Clone an existing project

To perform any actions on your project, you have to clone your project locally. You can do this by selecting from the list of projects.

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

## Create a project

You can also create a project from the CLI. First, create a directory inside which you will initialize your project.&#x20;

```bash
mdkir cli-project
cd cli-project
```

Inside your project directory, you can initialize a new project.&#x20;

```
redbrick init
    > Name: cli-project
    > Label: 
      IMAGE_ITEMS
      DICOM_SEGMENTATION
      ...
    > Taxonomy: 
      category-list-1
      category-list-2
      ...
    > Reviews: 2
```

* Name: Enter the name of your project.&#x20;
* Label: Define the type of your project e.g. DICOM\_SEGMENTATION
* Taxonomy: Select the taxonomy you're going to use for this project
* Review: Select how many review stages you'd like to add to this workflow e.g. 2
