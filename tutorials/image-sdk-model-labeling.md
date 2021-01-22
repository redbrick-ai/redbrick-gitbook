# SDK model labeling

## Image SDK model labeling

This code example will cover how to use the Python SDK to generate pre-labels using the [Remote Labeling](https://docs.redbrickai.com/sdk/remote-labeling/) module. For this example, we are going to be using Yolo v3 to be generating pre-labels on data. You can replace this with any other model, algorithm or rule based system. Make sure whatever method you use for generating pre-labels, produces classes with the same [Taxonomy](https://docs.redbrickai.com/platform/warehouse/warehouse/#taxonomies) as the project you've created.

### Requirements <a id="requirements"></a>

Before actually going through the code example, there are a few requirement/pre-requisites.

* Create a project that has a `remote-labeling` stage in it. Because we're using YOLO v3 for this example, we're going to assume this project was created with the YOLO taxonomy.
* Generate an api key for use with the sdk.
* Download the YOLO configuration files. Class names file [`coco.names`](https://github.com/pjreddie/darknet/blob/master/data/coco.names), net config file [`yolov3.cfg`](https://github.com/pjreddie/darknet/blob/master/cfg/yolov3.cfg), net weight file [`yolov3.weights`](https://pjreddie.com/media/files/yolov3.weights)
* Set up your directory as follows:

```text
folder
├── yolo
│   ├── coco.names
│   ├── yolov3.weights
│   └── yolov3.cfg
└── main.py
```

### Code <a id="code"></a>

The example below includes a few helper functions for loading the YOLO model and generating predictions. It then gets a single task from the remote-labeling stage, and generates predictions on that single task. The task along with the model generated labels are submitted to the backend.

```python
# main.py
import cv2
import numpy as np
import json
import redbrick
from redbrick.entity.label.bbox import ImageBoundingBox

def load_yolo():
    """
    Load the YOLO model.

    Loads the YOLO model using OpenCV, and return the net object
    along with other important details
    """
    net = cv2.dnn.readNet("yolo/yolov3.weights", "yolo/yolov3.cfg")
    classes = []
    with open("yolo/coco.names", "r") as f:
        classes = [line.strip() for line in f.readlines()]

    layers_names = net.getLayerNames()
    output_layers = [layers_names[i[0] - 1] for i in net.getUnconnectedOutLayers()]
    return net, classes, output_layers

def detect_objects(img, net, outputLayers):
    """Performs detection using YOLO on a single image."""
    blob = cv2.dnn.blobFromImage(
        img,
        scalefactor=0.00392,
        size=(320, 320),
        mean=(0, 0, 0),
        swapRB=True,
        crop=False,
    )
    net.setInput(blob)
    outputs = net.forward(outputLayers)
    return blob, outputs

def get_box_dimensions(outputs, height, width):
    """Parse the net prediction outputs to return bbox details."""
    boxes = []
    confs = []
    class_ids = []
    for output in outputs:
        for detect in output:
            scores = detect[5:]
            class_id = np.argmax(scores)
            conf = scores[class_id]
            if conf > 0.3:
                center_x = int(detect[0] * width)
                center_y = int(detect[1] * height)
                w = int(detect[2] * width)
                h = int(detect[3] * height)
                x = int(center_x - w / 2)
                y = int(center_y - h / 2)
                boxes.append([x, y, w, h])
                confs.append(float(conf))
                class_ids.append(class_id)
    return boxes, confs, class_ids



def main(api_key, org_id, project_id):
    """Main function."""
    # Init redbrick-sdk
    redbrick.init(api_key=api_key)
    remote_labeling = redbrick.remote_label.RemoteLabel(
        org_id=org_id, project_id=project_id, stage_name="<stage_name>"
    )

    # Get task from RedBrick AI
    tasks = remote_labeling.get_task(num_tasks=1)
    image = tasks[0].get_data(presigned_url=tasks[0].items_list_presigned[0])

    image = np.flip(image, axis=2)  # cv2 requires BGR
    image_height, image_width, _ = image.shape
    cv2.resize(image, None, fx=0.4, fy=0.4)

    # Generate predictions from YOLO
    model, classes, colors, output_layers = load_yolo()
    blob, outputs = detect_objects(image, model, output_layers)
    boxes, confs, class_ids = get_box_dimensions(outputs, image_height, image_width)

    # Submit task to RedBrick AI
    labels = []
    for idx, box in enumerate(boxes):
        x, y, w, h = box
        x /= image_width
        y /= image_width
        w /= image_width
        h /= image_height
        classname = str(classes[class_ids[idx]])
        category = [["object", classname]]
        entry = {
            "category": category,
            "bbox2d": {"xnorm": x, "ynorm": y, "wnorm": w, "hnorm": h},
        }
        labels.append(entry)

    image_bbox = ImageBoundingBox(labels=labels)
    remote_labeling.submit_task(task=tasks[0], labels=image_bbox)

if __name__ == "__main__":
    API_KEY = "<api_key>"
    ORG_ID = "<org_id>"
    PROJECT_ID = "<project_id>"

    main(API_KEY, ORG_ID, PROJECT_ID)
```

## Video SDK Model Labeling

This code example will cover how to use the Python SDK to generate pre-labels using the [Remote Labeling](https://docs.redbrickai.com/sdk/remote-labeling/) module. For this example, we are going to be using Yolo v3 to be generating pre-labels on video data. You can replace this with any other model, algorithm or rule based system. Make sure whatever method you use for generating pre-labels, produces classes with the same [Taxonomy](https://docs.redbrickai.com/platform/warehouse/warehouse/#taxonomies) as the project you've created.

### Requirements <a id="requirements"></a>

Before actually going through the code example, there are a few requirement/pre-requisites.

* Create a project that has a `remote-labeling` stage in it. Because we're using YOLO v3 for this example, we're going to assume this project was created with the YOLO taxonomy.
* Generate an api key for use with the sdk.
* Download the YOLO configuration files. Class names file [`coco.names`](https://github.com/pjreddie/darknet/blob/master/data/coco.names), net config file [`yolov3.cfg`](https://github.com/pjreddie/darknet/blob/master/cfg/yolov3.cfg), net weight file [`yolov3.weights`](https://pjreddie.com/media/files/yolov3.weights)
* Set up your directory as follows:

```text
folder
├── yolo
│   ├── coco.names
│   ├── yolov3.weights
│   └── yolov3.cfg
└── main.py
```

### Code <a id="code"></a>

The example below includes a few helper functions for loading the YOLO model and generating predictions. It then gets a single task from the remote-labeling stage, and generates predictions on that single task. The task along with the model generated labels are submitted to the backend.

```python
# main.py
import cv2
import numpy as np
import json
import redbrick
from redbrick.entity.label.bbox import VideoBoundingBox

def load_yolo():
    """
    Load the YOLO model.

    Loads the YOLO model using OpenCV, and return the net object
    along with other important details
    """
    net = cv2.dnn.readNet("yolo/yolov3.weights", "yolo/yolov3.cfg")
    classes = []
    with open("yolo/coco.names", "r") as f:
        classes = [line.strip() for line in f.readlines()]

    layers_names = net.getLayerNames()
    output_layers = [layers_names[i[0] - 1] for i in net.getUnconnectedOutLayers()]
    return net, classes, output_layers

def detect_objects(img, net, outputLayers):
    """Performs detection using YOLO on a single image."""
    blob = cv2.dnn.blobFromImage(
        img,
        scalefactor=0.00392,
        size=(320, 320),
        mean=(0, 0, 0),
        swapRB=True,
        crop=False,
    )
    net.setInput(blob)
    outputs = net.forward(outputLayers)
    return blob, outputs

def get_box_dimensions(outputs, height, width):
    """Parse the net prediction outputs to return bbox details."""
    boxes = []
    confs = []
    class_ids = []
    for output in outputs:
        for detect in output:
            scores = detect[5:]
            class_id = np.argmax(scores)
            conf = scores[class_id]
            if conf > 0.3:
                center_x = int(detect[0] * width)
                center_y = int(detect[1] * height)
                w = int(detect[2] * width)
                h = int(detect[3] * height)
                x = int(center_x - w / 2)
                y = int(center_y - h / 2)
                boxes.append([x, y, w, h])
                confs.append(float(conf))
                class_ids.append(class_id)
    return boxes, confs, class_ids


def main(api_key, org_id, project_id):
    """Main function for video remote-labeling."""
    # Init redbrick-sdk
    redbrick.init(api_key=api_key)
    remote_labeling = redbrick.remote_label.RemoteLabel(
        org_id=org_id, project_id=project_id, stage_name="LABEL"
    )

    # Get task from RedBrick AI
    tasks = remote_labeling.get_task(num_tasks=1)
    task = tasks[0]

    # Iterate through frames of video and generate YOLO preds
    labels = []
    model, classes, colors, output_layers = load_yolo()
    for frameindex, item in enumerate(task.items_list_presigned):
        frame = task.get_data(item)  # get frame data
        frame_height, frame_width, _ = frame.shape
        cv2.resize(frame, None, fx=0.4, fy=0.4)

        # Generate predictions from YOLO
        blob, outputs = detect_objects(frame, model, output_layers)
        boxes, confs, class_ids = get_box_dimensions(outputs, frame_height, frame_width)

        # Iterate over labels generated for frame and append to labels object
        for idx, box in enumerate(boxes):
            x, y, w, h = box
            x /= frame_width
            y /= frame_width
            w /= frame_width
            h /= frame_height
            x = np.max(x, 0)
            y = np.max(y, 0)
            w = np.max(w, 0)
            h = np.max(h, 0)
            classname = str(classes[class_ids[idx]])
            category = [["object", classname]]
            entry = {
                "category": category,
                "bbox2d": {"xnorm": x, "ynorm": y, "wnorm": w, "hnorm": h},
            }
            entry["frameindex"] = frameindex
            labels.append(entry)

    # Create label object, and submit task to RedBrick backend
    vid_bbox = VideoBoundingBox(labels=labels)
    remote_labeling.submit_task(task=tasks[0], labels=vid_bbox)


if __name__ == "__main__":
    API_KEY = "<api_key>"
    ORG_ID = "<org_id>"
    PROJECT_ID = "<project_id>"

    main(API_KEY, ORG_ID, PROJECT_ID)
```

