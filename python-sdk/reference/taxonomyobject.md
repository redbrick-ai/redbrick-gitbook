# TaxonomyObject

## Taxonomy V2

```typescript
type Taxonomy = {
    orgId: string;
    name: string;
    createdAt: datetime;
    archived: boolean;
    isNew: true;
    taxId: string;
    studyClassify: Attribute[];
    seriesClassify: Attribute[];
    instanceClassify: Attribute[];
    objectTypes: ObjectType[];
}

type ObjectType = {
    category: string;
    classId: number; // [0, n)
    labelType: BBOX | POINT | POLYLINE | POLYGON | ELLIPSE | SEGMENTATION | LENGTH | ANGLE;
    attributes?: Attribute[];
    color?: string;
    archived?: boolean;
    parents?: string[];
    hint?: string;
}

type Attribute = {
    name: string;
    attrType: BOOL | TEXT | SELECT | MULTISELECT;
    attrId: number;
    options?: AttributeOption[];
    archived?: boolean;
    parents?: string[];
    hint?: string;
}

type AttributeOption = {
    name: string;
    optionId: number;
    color?: string;
    archived?: boolean;
}
```

## Taxonomy V1

RedBrick AI no longer supports the creation of Taxonomies V1.
