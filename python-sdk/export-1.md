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
    json.dump(file_, result, indent=2)
```



