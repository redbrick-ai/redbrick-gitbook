---
description: Types that are common across the SDK
---

# Reference

### TaxonomyObject

```text
{
    "name": str,
    "version": int,
    "categories": [CategoryObject],
    "attributes": [AttributeObject]
}

CategoryObject
{
    "name": str,
    "classId": int,
    "children": [CategoryObject]
}

AttributeObject
{
    "name": str,
    "attrType": str
}
```

### LabelObject

```text
{
    "category": [[str]],
    "attributes": [LabelAttribute],
    "labelid": str,
    "bbox2d": null or {BBox2d},
    "polygon": null or [Point],
    "polyline": null or [Point],
    "point": null or Point,
    "ellipse": null or {Ellipse},
    "pixel": null or {Pixel},
    
}

LabelAttribute
{
    "name": str,
    "value": any
}

BBox2d 
{
    "xnorm": float, # [0, 1]
    "ynorm": float,
    "wnorm": float,
    "hnorm": float 
}


Point
{
    "xnorm": float,
    "ynorm": float
}

Ellipse
{
    "xnorm": float,
    "ynorm": float,
    "wnorm": float,
    "hnorm": float,
    "rot": float,  # [0, pi)
}


```

