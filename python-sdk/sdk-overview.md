# SDK Overview

The RedBrick Python SDK is a tool to interact programmatically with the RedBrick AI platform. The SDK is a developer friendly way to carry out important operations like data and label export.

{% hint style="info" %}
The RedBrick SDK works on Mac, windows, and linux, and is available on [pypi](https://pypi.org/project/redbrick-sdk/). The SDK is compatible with **Python 3.6.0+.** 
{% endhint %}

### Getting Started

Follow the steps below to get started with the RedBrick SDK.

**Step 1: Generate an api key**

You can create an API key for your organization under _Organization Settings_, which is accessible by clicking on the bottom left corner of the screen.

Once you create an API key, make sure to store it safely, because you will not be able to look up the key value once you close the dialog box.

**Step 2: Install the RedBrick SDK**

You can install the SDK by using pip.

```bash
$ pip3 install -U redbrick-sdk
```

**Step 3: Initialize the RedBrick SDK in Python**

To use the SDK, you need to get your project. Fill in your own values in the following script to start off any session.

```python
import redbrick

api_key = "<your api key from step 2>"
url = "https://api.redbrickai.com"
org_id = "<>"
project_id = "<>"
project = redbrick.get_project(api_key, url, org_id, project_id)
```

Now that you have the project object, go to the other sections of this SDK guide to perform specific actions.



