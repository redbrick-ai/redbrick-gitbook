---
description: Reference types that are common across the SDK are documented on this page.
---

# Reference

## Label Objects

Useful for understanding the RedBrick label format used for exports and label imports. 

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

All **ynorm **values are y co-ordinates normalized by the height of the image. 
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
