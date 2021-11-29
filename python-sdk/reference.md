---
description: Reference types that are common across the SDK are documented on this page.
---

# Format Reference

## RedBrick AI Export Format

```json
[
  {
    "name": "image_name", // same unique name used on upload
    "items": ["image/url.png"], // image url, or frame urls
    "itemsPresigned": ["image/url_presigned.png"], // same as above, but signed urls
    "createdBy": "email@email.com",
    "taskId": "123", // unique id assigned to each task

    "labels": [LabelObject]
  },
]
```

## LabelObject

Useful for understanding the RedBrick label format used for exports and label imports.&#x20;

```javascript
// LabelObject
{
    "category": [["object", str]], // String must belong to Project Taxonomy
    "attributes": [LabelAttribute],
    "labelid": str, // Uniqye for every label 
    
    "bbox2d": null or {BBox2d},
    "polygon": null or [Point],
    "polyline": null or [Point],
    "point": null or Point,
    "ellipse": null or {Ellipse},
    "pixel": null or {Pixel},
    
    // only included if you have classification labels    
    "frameclassify": null or bool,
    "taskclassify": null or bool,

    // only inlcluded for video projects
    "frameindex": null or int,
    "trackid": null or str, // unique id for an object track across frames
    "keyframe": null or bool, // True if manually labeled, False if interpolated
    "end": null or bool //  True if this label is the last label of a track.
}

// LabelAttribute
{
    "name": str,
    "value": any
}

// BBox2d
{
    "xnorm": float, // [0, 1]
    "ynorm": float,
    "wnorm": float,
    "hnorm": float 
}

// Point
{
    "xnorm": float,
    "ynorm": float
}

// Ellipse
{
    "xcenternorm": float,
    "ycenternorm": float,
    "xnorm": float,
    "ynorm": float,
    "rot": float, // [0, pi) radians
}

// Pixel 
{
    "imagesize": [int, int], // width, height in pixels,
    "regions": [[[int, int]]],
    "holes": null or [[[int, int]]]
}

```

{% hint style="info" %}
All **xnorm** values are x co-ordinates normalized by the width of the image.

All **ynorm** values are y co-ordinates normalized by the height of the image.&#x20;
{% endhint %}

{% hint style="info" %}
The `LabelObject` requires at least one of the label type fields  - `bbox2d`, `polygon`, `polyline`, `point`, `ellipse`, `pixel, taskclassify: true` entries. The entries must match the label type of your Project.
{% endhint %}

## Taxonomy Objects

```javascript
// TaxonomyObject
{
    "name": str,
    "version": int,
    "categories": [CategoryObject],
    "attributes": [AttributeObject]
}

// CategoryObject
{
    "name": str, // must be a part of the Project Taxonomy
    "classId": int, // [0, n) where n is number of categories
    "children": [CategoryObject]
}

// AttributeObject
{
    "name": str,
    "attrType": str
}
```

## Task Objects

```javascript
// TaskObject
{
     "taskId": str, // unique id
     "labels": [LabelObject],  
     "items": [str], // Unsigned URL's 
     "itemsPresigned": [str],  // Signed URL's to download images
     "name": str  // unique name given when creating a datapoint
}
```

## PNG Mask Formats

For exporting to masks, or importing masks to RedBrick AI projects, you have to follow the formats outlined in this section. The masks directory will have the following structure:

```shell
# On Export, the directory will be named after your project_id
# On Upload, you can name the directory whatever you like. 

project_id 
├── uuid_1.png # On Export, masks file name will be the unique task_id. 
├── uuid_2.png # On Upload, mask file name will be used as the datapoint name.
├── uuid_3.png
├── datapoint_map.json # Map from mask filename -> image items path
└── class_map.json # Map from object category -> mask color
```

**PNG Masks**

The masks will be RGB PNG's with 8 bit integer pixel values `[0, 255]` (the corresponding class can be found the `class_map.json`).&#x20;

**Class Map**

The mask PNG's are 3 channel RGB images. The mapping from RGB values to category names is provided in the `class_map.json`.&#x20;

```json
// class_map.json
{
    "category_1": [1, 10, 2] // rgb values [0, 255]
    "category_2": [29, 198, 22]
    .
    .
}
```

**Datapoint Map**

The `datapoint_map.json` file contains a mapping between the mask filename and the corresponding image file path. The `datapoint_map.json` will be the following format:&#x20;

* Keys
  * Name of your PNG masks, which will be the unique `task_id` field.
* Values
  * &#x20;The [items field](../projects/importing-data/#items-list) that was used on upload. If Direct Upload was used, this will be a string with your original filename at the end of the string for e.g. `uuid/images/uuid/your_file_name.png`.

```json
// datapoint_map.json
{
    "mask_file_name_1.png": "https://path_to_my_image_1.png", 
    "mask_file_name_2.png": "https://path_to_my_image_2.png", 
    .
    .
}
```

