# Importing data and labels

You can programmatically upload your data to the RedBrick AI platform and also upload pre-labels with the data so that your team can correct the annotations on the platform.&#x20;

## Creating data points without labels

You can use the `create_datapoints` method to upload data to the RedBrick AI platform.&#x20;

Perform standard SDK set up to create an RBProject object.

```python
import redbrick

# Standard Setup
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"

project = redbrick.get_project(api_key, url, org_id, project_id)
```

Construct your data points object and upload to RedBrick.

```python
# Your storage id can be found on the Storage Methods tab (left sidebar) on RedBrick AI
# redbrick.StorageMethod.REDBRICK is for locally stored data.
storage_id = redbrick.StorageMethod.REDBRICK

datapoints = [
    {
        # Must be unique for each datapoint.
        "name": "my first upload",
        
        # Must be a valid path to data stored in the storage method
        # defined above.
        "items": [
            "path/to/local/file.png"
        ]
    }
]

project.upload.create_datapoints(storage_id, datapoints)
```

## Creating data points with vector labels

You can also upload data with pre-labels using the `create_datapoints` method.

```python
# Your storage id can be found on the Storage Methods tab (left sidebar) on RedBrick AI
# redbrick.StorageMethod.PUBLIC is for publically stored data.
storage_id = redbrick.StorageMethod.PUBLIC

datapoints = [
    {
        # Must be unique for each datapoint.
        "name": "my first upload",
        
        # Must be a valid path to data stored in the storage method
        # defined above.
        "items": [
            "http://datasets.redbrickai.com/car-vids/car-1/frame20.png"
        ]
        
        # The labels field needs to be of type LabelObject
        "labels": [
            {
                # category-name must be a valid name part of your
                # project taxonomy.
                "category": [["object", "category-name"]],
                
                "bbox2d": {
                    "xnorm": 0.1,
                    "ynorm": 0.1,
                    "wnorm": 0.2,
                    "hnorm": 0.2
                }
            }
        ]
    }
]

project.upload.create_datapoints(storage_id, datapoints)
```

{% hint style="info" %}
Please see the [reference documentation for the LabelObject format](reference.md#labelobject).
{% endhint %}

## Creating data points with segmentation labels

To upload data with masks labels, you can use the `create_datapoint_from_masks` method. You have to first prepare a directory containing your masks in the format defined in the [reference documentation](reference.md#png-mask-formats).

```python
# Directory containing the mask data, in the correct format.
dir = "<TODO>" 

# Load map information
with open(os.path.join(dir, "class_map.json"), "r") as file:
    class_map = json.load(file)
with open(os.path.join(dir, "datapoint_map.json"), "r") as file:
    datapoint_map = json.load(file)

# Iterate over files, and upload data with masks. 
for file in datapoint_map:
    mask_im = Image.open(os.path.join(dir, file))
    mask = np.array(mask_im)[:, :, 0:3] # Ignore Alpha channel
    mask = mask.astype(np.uint8)
    
    # Because we are using redbrick.StorageMethod.REDBRICK, 
    # the image_path will need to be path to a locally stored image. 
    image_path = datapoint_map[file]
    project.upload.create_datapoint_from_masks(
        redbrick.StorageMethod.REDBRICK, mask, class_map, image_path
    )
```
