---
description: Reference types that are common across the SDK are documented on this page.
---

# Reference

## Label Objects

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
    
    
    "frameclassify": null or bool,
    "taskclassify": null or bool,

    "frameindex": null or int,
    "trackid": null or str,
    "keyframe": null or bool,
    "end": null or bool
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
All **xnorm **values are x co-ordinates normalized by the width of the image.

All **ynorm **values are y co-ordinates normalized by the height of the image.&#x20;
{% endhint %}

{% hint style="info" %}
The `LabelObject` requires at least one of the label type fields  - `bbox2d`, `polygon`, `polyline`, `point`, `ellipse`, `pixel, taskclassify: true `entries. The entries must match the label type of your Project.
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
├── uuid_1.png # On Export, masks will be exported a unique id for each datapoint.
├── uuid_2.png # On Upload, mask file name will be used as the datapoint name.
├── uuid_3.png
├── datapoint_map.json # Map from mask filename -> image items path
└── class_map.json # Map from object category -> mask color
```

**Class Map**

The mask PNG's are 3 channel RGB images. The mapping from RGB values to category names is provided in the `class_map.json`.&#x20;

```json
// class_map.json
{
    "category_1": [0.90, 0.33, 0.05] // rgb values [0, 1]
    "category_2": [0.12, 0.88, 0..]
    .
    .
}
```

**Datapoint Map**

_When you export_ your data as masks, the `datapoint_map.json` file will contain a mapping between the mask filename (the filename will be a unique identifier), to the [items field](../projects/importing-data/#items-list) used on upload. If you have used direct upload, the items field will be a file path with your image filename at the end of the string, e.g. `uuid/images/uuid/your_file_name.png`).

_When you import _your masks, the name of your mask files will be used as your datapoint's name on the RedBrick AI platform. These **names must be unique across your entire project. **The `datapoint_map.json` must contain a mapping between these unique filenames and the [items path](../projects/importing-data/#items-list) that will be used for your upload.&#x20;

{% hint style="info" %}
Uploading masks with Direct Upload is not supported right now. If you want to upload your masks with your image data, [please use an external storage method](../projects/importing-data/#storage-methods).&#x20;
{% endhint %}

```json
// datapoint_map.json
{
    "mask_file_name_1.png": "https://path_to_my_image_1.png", 
    "mask_file_name_2.png": "https://path_to_my_image_2.png", 
    .
    .
}
```

