# SDK Overview

The RedBrick Python SDK is a tool to interact programmatically with the RedBrick AI platform. The SDK is a developer friendly way to carry out important operations like data and label export.

{% hint style="info" %}
The RedBrick SDK works on Mac, windows, and linux, and is available on [pypi](https://pypi.org/project/redbrick-sdk/). The SDK is compatible with **Python 3.6.0+. **
{% endhint %}

### **Generate an API Key**

You can create an API key for your organization under _Organization Settings_, which is accessible by clicking on the bottom left corner of the screen.

### Install the RedBrick SDK

The `redbrick-sdk` is available on pypy and can be installed using pip.

```bash
$ pip3 install -U redbrick-sdk
```

### **Initialize the RedBrick SDK in Python**

To use the SDK, you need to get your project ID, and organization ID. Fill in your own values in the following script to start off any session.

```python
import redbrick

api_key = "<your api key from step 2>"
url = "https://api.redbrickai.com"
org_id = "<>"
project_id = "<>"
project = redbrick.get_project(api_key, url, org_id, project_id)
```

The `project_id` and `org_id` is available in the URL when you are logged into your project - `https://app.redbrickai.com/<orgid>/projects/<projectid>`.

## Running inside of a Jupyter Notebook

Under the hood, the Python SDK uses advanced language features to optimize for performance. Certain aspects of these do not play nicely with Jupyter notebooks or other complex python environments.

If you see an error similar to `RuntimeError: asyncio.run() cannot be called from a running event loop` you may be able to fix this by utilizing the `nest_asyncio`  package at the top of your notebook. This comes standard with most Jupyter notebook installs. 

```python
import nest_asyncio
nest_asyncio.apply()
```
