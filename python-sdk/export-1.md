---
description: Programmatically exporting data from your RedBrick AI Project.
---

# Export

### Standard Export in RedBrick AI format

```python
import json
import redbrick

# Standard Setup
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
project = redbrick.get_project(api_key, url, org_id, project_id)

# Get all data
result = project.export.redbrick_format()

# Write to file
with open("redbrick_export.json", "w+") as file_:
    json.dump(result, file_, indent=2)
```



### Export to Coco format

The MS Coco file format is used broadly across the computer vision field so we offer it as a standard export for projects that are doing image detection for bounding box shapes and polygon shapes.

```python
import json
import redbrick

# Standard Setup
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"
project_id = "<TODO>"
project = redbrick.get_project(api_key, url, org_id, project_id)

# Get all data
result = project.export.coco_format()

# Write to file
with open("redbrick_coco_export.json", "w+") as file_:
    json.dump(result, file_, indent=2)
```



