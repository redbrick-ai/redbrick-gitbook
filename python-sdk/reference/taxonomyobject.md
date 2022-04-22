# TaxonomyObject

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
