---
description: Beta release on https://preview.redbrickai.com
---

# Heat maps

Heatmaps provide a way to overlay scalar volumetric data over the base image for reference purposes. You will have the ability to adjust the multiple color gradients and thresholding options to visualize the data.

{% hint style="info" %}
Heatmaps must be uploaded via the SDK.&#x20;
{% endhint %}

## Format:

```typescript
type Series {
  ...
  heatMaps: [HeatMap]
}

type HeatMap {
  name: string;
  item: string; // file path
  preset?: string;
  dataRange?: [number, number];
}
```

For the complete task format, please refer to [https://sdk.redbrickai.com/formats/index.html](https://sdk.redbrickai.com/formats/index.html)

## Upload

Please install the pre-release version of the RedBrick SDK (`pip install redbrick-sdk==2.17.7b1`)

Here is a sample script to upload heat-maps in task.

```python
from typing import List

import redbrick
from redbrick.types.task import InputTask


ORG_ID = "ORG_ID"
PROJECT_ID = "PROJECT_ID"
API_KEY = "API_KEY"
URL = "https://preview.redbrickai.com"

project = redbrick.get_project(ORG_ID, PROJECT_ID, API_KEY, URL)

points: List[InputTask] = [
    {
        "name": "sdk-public",
        "series": [
            {
                "items": [
                    "/path/to/image/inst1.dcm",
                    "/path/to/image/inst2.dcm",
                    "/path/to/image/inst3.dcm",
                ],
                "heatMaps": [
                    {"name": "heatmap 1", "item": "/path/to/heatmap1.nii.gz"},
                    {"name": "heatmap 2", "item": "/path/to/heatmap2.nii.gz"},
                ],
            }
        ],
    }
]

project.upload.create_datapoints(redbrick.StorageMethod.REDBRICK, points)
```

## Visualization

Visualization settings can be toggled under the Visualization panel on the right sidebar.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-06-13 at 6.40.16 PM.png" alt=""><figcaption></figcaption></figure>
