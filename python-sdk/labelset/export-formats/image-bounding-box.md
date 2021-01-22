# Image Bounding Box

For labelsets with `task_type == BBOX` and `data_type == IMAGE` the following export format types are supported:

* redbrick
* yolo

### redbrick <a id="redbrick"></a>

The `redbrick` format is the default export format and is the same as the standard `yolo` format which is covered below.

### yolo <a id="yolo"></a>

The `yolo` format follows the popular format for the Yolo v2, v3 object detection networks, which is covered in the link [here](https://github.com/AlexeyAB/darknet). The output folder where the data and labels are exported will be structured as follows:

```text
Export_folder
├── obj_train_data
│    ├── path_to_data_1.jpg
│    ├── path_to_data_1.txt
│    .
│    .
│    .
├── obj.data
├── obj.names
└── train.txt
```

**obj\_train\_data**

This folder will contain a `.txt`-file for each `.jpg`-file with the same name. The name of the files will be the same as the `url` field of the `items_list` that was used to upload these datapoints \(all the `/` characters will be replaced by `_`\). There will be a new line in the `.txt` file for each object in the following format:

`<object-class> <x-top-left> <y-top-left> <width> <height>`

Where `<object-class>` is an index of the classes enumerated in `obj.names`, and the coordinates of the bounding box are normalized values: `<x-top-left>` and `width` are normalized by the width of the image and `<y-top-left>` and `height` are normalized by the height of the image.

**obj.data**

This file contains information of the filenames in the current directory.

**obj.names**

This file contains a list of all the object classes in the dataset. It is a flattended version of the Taxonomy of the dataset.

**train.txt**

This file contains a list of all the image filepaths in the `obj_train_data` directory.

### coco <a id="coco"></a>

A detailed overview of the COCO output format can be found on the [COCO website](https://cocodataset.org/#format-data). If you choose to export data in the coco format the output folder will be structured as follows:

```bash
Export_folder
├── annotations
│    ├── images_info_train.json
│    └── instances_train.json
└── images
     ├── path_to_data_1.jpg
     ├── path_to_data_2.jpg
     .
     .
     .
```

**images\_info\_train.json**

Your image and label information is all available in the `images_info_train.json` file, which has the following format:

```javascript
{
    "info": info,
    "images": [image],
    "annotations": [annotation],
    "licenses": [license],
    "categories": [categories]
}

info{
    "year": int,
    "version": str,
    "description": str,
    "contributor": str,
    "url": str,
    "date_created": datetime,
}

image{
    "id": int,
    "width": int,
    "height": int,
    "file_name": str,
    "license": int,
    "flickr_url": str,
    "coco_url": str,
    "date_captured": datetime,
}

license{
    "id": int,
    "name": str,
    "url": str,
}

annotation{
    "id": int,
    "image_id": int,
    "category_id": int,
    "area": float,
    "bbox": [x,y,width,height], # x,y are the location of the top left of the bbox
                                # width, height are width and height of bbox
                                # all values are in pixels
    "iscrowd": 0 or 1,
}

categories[{
    "id": int,
    "name": str,
    "supercategory": str,
}]
```

