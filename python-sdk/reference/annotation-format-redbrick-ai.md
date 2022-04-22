# Annotation Format RedBrick AI

## RedBrick AI Format

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

{% hint style="success" %}
See [LabelAttribute](taxonomyobject.md)
{% endhint %}

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
    "frameindex": null or int, // 0 -> len(frames) - 1 
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
All **`xnorm` ** values are x co-ordinates normalized by the width of the image.

All **`ynorm` ** values are y co-ordinates normalized by the height of the image.&#x20;
{% endhint %}

{% hint style="info" %}
The `LabelObject` requires at least one of the label type fields  - `bbox2d`, `polygon`, `polyline`, `point`, `ellipse`, `pixel, taskclassify: true` entries. **The entries must match the Label type of your Project**.
{% endhint %}
