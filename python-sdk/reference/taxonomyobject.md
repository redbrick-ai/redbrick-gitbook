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
}

type Attribute = {
    name: string;
    attrType: BOOL | TEXT | SELECT | MULTISELECT;
    attrId: number;
    options?: AttributeOption[];
    archived?: boolean;
}

type AttributeOption = {
    name: string;
    optionId: number;
    color?: string;
    archived?: boolean;
}
```

## Taxonomy V1

```typescript
type Taxonomy = {
    orgId: string;
    name: string;
    createdAt: datetime;
    archived: boolean | null;
    isNew: false;
    version: int;
    categories: Category[];
    attributes: Attribute[];
    taskCategories: Category[] | null;
    taskAttributes: Attribute[] | null;
    colorMap: Color[] | null;
}

type Category = {
    name: string;
    classId?: int; // present for all except root ("object")
    disabled?: boolean | null;
    children?: Category[]
}

type Attribute = {
    name: string;
    attrType: BOOL | TEXT | SELECT | MULTISELECT;
    whitelist: str[][] | null;
    disabled: boolean | null;
}

type Color = {
    name: string;
    color: string;
    classid: int;
    trail: string[];
    taskCategory: boolean;
}
```
