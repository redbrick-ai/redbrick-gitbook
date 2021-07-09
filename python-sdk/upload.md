---
description: Programmatically uploading data to your RedBrick AI Project.
---

# Upload

### Full script

If you just want to get started quickly, fill in your own values in this script.

```python
import redbrick

api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)

# default public storage method
storage_id = "11111111-1111-1111-1111-111111111111"

datapoints = [
    {
        "name": "my first upload",
        "items": [
            "http://datasets.redbrickai.com/car-vids/car-1/frame20.png"
        ]
    }
]
failed_to_create = project.upload.create_datapoints(storage_id, datapoints)

for point in failed_to_create:
    print(point["error"])
```

### 1. Get storage\_id

You must first tell your RedBrick AI project where the data you are uploading is stored. If you have not yet configured your storage, see [Importing data](../projects/importing-data/).

Otherwise, get your intended storage\_id from the storage tab of your organization.

For this example, we will use the default "Public" storage method. This means that the urls we will be uploading can be accessed publicly without altercation.

```python
# default public storage method
storage_id = "11111111-1111-1111-1111-111111111111"
```

### 2. Prepare Data

The items list format for uploading via the SDK is the same as the format for file uploads shown on [Importing data](../projects/importing-data/).

{% hint style="info" %}
The fastest way to modify this script, is your get some public hosted images \(google or flickr\) and replace the url in the _items_ field.
{% endhint %}

```python
datapoints = [
    {
        "name": "my first upload",
        "items": [
            "http://datasets.redbrickai.com/car-vids/car-1/frame20.png"
        ]
    }
]
```

{% hint style="danger" %}
The name field should be unique across a single project. This is done to prevent you from uploading the same image multiple times.
{% endhint %}

### 3. Upload the data and check for errors

```python
failed_to_create = project.upload.create_datapoints(storage_id, datapoints)

for point in failed_to_create:
    print(point["error"])
```



