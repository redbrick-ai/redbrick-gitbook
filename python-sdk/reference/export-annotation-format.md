# Export Annotation Format

## Export Folder Structure

RedBrick AI exports annotations in a JSON structure, accompanied by [NIfTI-1 masks](https://nifti.nimh.nih.gov/nifti-1/) for segmentations. All data will be exported within a folder named after your `project_id`, with the following structure:

```
project_id/
├── segmentations
│   ├── study01
│   │   └── series1.nii
│   └── study02
│       ├── series1.nii
│       └── series2.nii
└── tasks.json
```

## Segmentations Directory

The segmentation directory will contain a single sub-directory for each task in your export. The sub-directories will be named after the task [`name`](export-annotation-format.md#name-string). A single task (depending on whether it was single series or multi-series) can have one or more segmentations.

The individual segmentation files will be in NIfTI-1 format and be [named after the user-defined series name](export-annotation-format.md#name-string-1). If no series name is provided on upload, RedBrick will assign a unique name. Corresponding meta-data ex. category names will be provided in [tasks.json](export-annotation-format.md#tasks-json).

## Tasks JSON

There will be a **single entry for each task** in the items file. Please see the definition (typescript) of the JSON object below:

```typescript
type Tasks = Task[];
​
// Single task on RedBrick can be single/multi-series
type Task = {
  // Required on upload and export
  name: string;
  series: Series[];
​
  // Task level annotation information
  classification?: Classification;
​
  // Not required on upload
  taskId?: string;
  currentStageName?: string;
  createdBy?: string;
  createdAt?: string;
  updatedBy?: string;
  updatedAt?: string;
  
  // assign metadata to a Task
  metaData?: { [key: string]: string }
  
  // Prescribe task assignent
  preAssign?: {
    [stageName: string]: string
  }
};
​
// A single series can be 2D, 3D, video etc.
type Series = {
  items: string | string[];
  name?: string;
​
  segmentations?: string | string[];
  segmentMap?: {
    [instanceId: string]: number | string | string[] | {
      category: number | string | string[];
      attributes?: Attributes;
    };
  };
  landmarks3d?: Landmarks3D[];
  measurements?: (MeasureLength | MeasureAngle)[];
  boundingBoxes?: BoundingBox[];
  polygons?: Polygon[];
  polylines?: Polyline[];
  classifications?: Classification[];
  instanceClassifications?: InstanceClassification[];
   metaData?: { [key: string]: string };
};
​
// Label Types
type Landmarks3D = {
  point: VoxelPoint;
  category: string | string[];
  attributes?: Attributes;
};
​
type MeasureLength = {
  type: 'length';
  point1: VoxelPoint;
  point2: VoxelPoint;
  absolutePoint1: WorldPoint;
  absolutePoint2: WorldPoint;
  normal: [number, number, number];
  length: number;
  category: string | string[];
  attributes?: Attributes;
};
​
type MeasureAngle = {
  type: 'angle';
  point1: VoxelPoint;
  point2: VoxelPoint;
  vertex: VoxelPoint;
  absolutePoint1: WorldPoint;
  absolutePoint2: WorldPoint;
  absoluteVertex: WorldPoint;
  normal: [number, number, number];
  angle: number;
  category: string | string[];
  attributes?: Attributes;
};
​
type BoundingBox = {
  pointTopLeft: Point2D;
  wNorm: number;
  hNorm: number;
  category: string | string[];
  attributes?: Attributes;
​
  // video meta-data
  video?: VideoMetaData;
};
​
type Polygon = {
  points: Point2D[];
​
  category: string | string[];
  attributes?: Attributes;
​
  // video meta-data
  video?: VideoMetaData;
};
​
type Polyline = {
  points: Point2D[];
  category: string | string[];
  attributes?: Attributes;
​
  // video meta-data
  video?: VideoMetaData;
};
​
type Classification = {
  category: string | string[];
​
  // video meta-data
  video?: VideoMetaData;
};
​
type InstanceClassification = {
  fileIndex: number;
  fileName?: string;
  values: { [attributeName: string] : boolean};
}

type Attributes =
  | { // Taxonomy V2 attributes
      attrId?: number;
      name?: string;
      optionId?: number | number[];
      value?: string | boolean | string[];
    }[]
  | { // Taxonomy V1 attributes
      [attributeName: string]: string | boolean | string[];
    };
​
type VideoMetaData = {
  frameIndex: number;
  trackId: string;
  keyFrame: number;
  endTrack: Boolean;
};
​
// i is rows, j is columns, k is slice
type VoxelPoint = {
  i: number;
  j: number;
  k: number;
};
// The position of VoxelPoint in physical space (world coordinate) computed using the Image Plane Module
type WorldPoint = {
  x: number;
  y: number;
  z: number;
};
type Point2D = {
  xnorm: number;
  ynorm: number;
};
```

### Task

The `Task` object represents a single task on RedBrick AI. It contains task-level meta-data information about all the series within the task. A task can contain a [single series or multiple series](../../annotation/layout-and-multiple-volumes/) (ex. a full MRI study).&#x20;

#### `name: string`

A user-defined string is defined on upload, it is _required to be unique_ across all tasks in your project. The `name` is meant to be a human-readable string that can help identify tasks ex. you can set `name` of a task to `patient/study01`.

#### `taskId?: string`

A RedBrick AI generated a unique identifier for each task. This value will be provided on export.

#### `currentStageName?: string`

The current stage this task is in is when it was exported.&#x20;

#### `createdBy?: string`

The e-mail of the user who uploaded this task.

#### `createdAt?: string`

The datetime this task was created (uploaded).

#### `updatedBy?: string`

The e-mail of the last user to make edits to this task.

#### `updatedAt?: string`

The datetime this task was last edited.

#### **`preAssign?: { [stageName : string] : string}`**

Prescribe during upload who will get a task assigned to them. You can define the assignment for each stage of the workflow, for example, Label and Review, `{"Label": "name1@redbrickai.com", "Review": "name2@redbrickai.com"}`.

#### `classification: { attributes : [string : boolean] }`

A list of attributes assigned to an entire task (or study, if the task encapsulates an entire study).

**`metaData?: { [key: string]: string }`**

A list of key value pairs that can be affixed to a Task.

### Series

The `Series` object has meta-data and annotations for a single series within a task. A series can represent a single MRI/CT series, a video, or a single 2D image. If a series has annotations, you can expect one or more of the label entries to be present i.e. `segmentations`, `polygons` etc.

#### `items: string | string[]`

The items entry is a list of file paths that point to your data. Please have a look at the [#items-list](../../importing-data/import-cloud-data.md#items-list "mention")documentation to understand how to format for various modalities and series/study uploads.

#### `name: string`

An optional user-defined string, _needs to be unique_ across all series. Individual [series will be named after this value on the labeling tool](https://www.loom.com/i/ea12e486bd8845d7b3b8a83fc115ad58). Exported segmentation files will also be named using this value. Using the Series Instance UID here is good practice. &#x20;

#### `classifications: { attributes: [string : boolean] }`

A list of attributes assigned to a specific Series.

#### `instanceClassifications: fileIndex | fileName | [ values: {string : boolean} ]`

The `instanceClassifications` object defines a series of boolean values that can be assigned to individual instances (e.g. frames in a video).

**`metaData?: { [key: string]: string }`**

A list of key value pairs that can be affixed to a Series.

### Common Label Keys

Here are the definition for some common entries present in some/all label entries.&#x20;

#### `category: string | string[]`

The class of your annotations. This value is part of your Project [Taxonomy](../../projects/taxonomies/). If the class is nested, `category` will be `string[]`.

#### `attributes: {[attributeName: string]: string | boolean}`

Each annotation can have accompanying attributes, that are also defined in your Project [Taxonomy](../../projects/taxonomies/). `attributeName` is defined when creating your Taxonomy.&#x20;

#### `VoxelPoint: {i: number, j: number, k: number}`

`VoxelPoint` represents a three-dimensional point in image space, where i and j are columns and rows, and k is the slice number.&#x20;

#### `WorldPoint: {x: number, y: number, j: number}`

`WorldPoint` represents a three-dimensional point in physical space/world coordinates. The world coordinates are calculated using `VoxelPoint` and the [Image Plane Module](https://dicom.nema.org/medical/dicom/current/output/chtml/part03/sect\_C.7.6.2.html).

#### `Point2D: {xnorm: number, ynorm: number}`

`Point2D` represents a two dimensional point. This is used to define annotation types on 2D data. `xnorm` has been normalized by image width, `hnorm` has been normalized by image height.

#### `fileIndex: number`

`fileIndex` is an integer that corresponds to a specific frame in a video series.

#### `fileName: string`

`fileName` represents the name given to an image or specific frame in a video series.

### Video Meta Data

#### `frameIndex: number` (video)

This specifies which frame in a video sequence the annotation was created.&#x20;

#### `trackId: string` (video)

A unique string that identifies distinct object tracks in a video sequence.

#### `keyFrame: boolean` (video)

If true, this annotation was manually added on a particular video sequence. If false, this annotation is a result of linear interpolation.

#### `endFrame: boolean` (video)

If true, the annotation is the last annotation for a particular video track segment.&#x20;

### Segmentation

#### `segmentations?: string | string[]`

A list of file paths of segmentation files for this series. Either a single `.nii` file, or multiple `.nii` files containing different instances.

**`segmentMap?: { [instanceId: number]: { category: string | string[]; attributes?: Attributes }};`**

A mapping between a segmentation's instance ID, your Taxonomy category name, and any accompanying attributes. The mapping will apply only to the current series, and instance IDs must be unique across all series in a task (this is useful for instance segmentation).

Please note that the `segmentMap`'s instanceId is generated **incrementally based on the order in which annotations were created by the labeler**. You can find an example JSON output below.&#x20;

```json
"items": ["image-file.ima",],
"segmentations": "./path/to/segmentation/file.nii.gz",
"segmentMap": {
  "1": {
    // This is the first annotation the labeler created
    "category": "Vertebral Body"
  },
  "2": {
    // This is the second annotation the labeler created
    "category": "Vertebral Body"
  },
  "3": {
    // This is the third annotation the labeler created
    "category": "Vertebral Body"
  },
  "4": {
    // This is the fourth annotation the labeler created
    "category": "Spinal Canal Mass"
  },
  "5": {
    // This is the fifth annotation the labeler created
    "category": "Disc Pathology"
  }
},

```

### BoundingBox

Represents a two-dimensional bounding box

#### `pointTopLeft:` [`Point2D`](export-annotation-format.md#point2d-xnorm-number-ynorm-number)

The location of the top-left point of the bounding box.

#### `wNorm, hNorm: number`

The width and height of the bounding box, normalized by the width and height of the image.

### Polygon

#### `points:` [`Point2D`](export-annotation-format.md#point2d-xnorm-number-ynorm-number)`[]`

A list of 2D points that are connected to form a polygon. This list is ordered such that, $$point_i$$ is connected to $$point_{i+1}$$. The last point is also connected to the first point to close the polygon.&#x20;

### MeasureLength

#### `point1, point2 :` [`VoxelPoint`](export-annotation-format.md#voxelpoint-i-number-j-number-k-number)

A length measurement is defined by two points, and the length measurement is the distance between the two points.

#### `absolutePoint1, absolutePoint2 :` [`WorldPoint`](export-annotation-format.md#worldpoint-x-number-y-number-j-number)

Corresponding to `point1`, `point2` these are points in physical space.

#### `normal: [number, number, number]`

Measurements can be made on oblique planes. `normal` defines the normal unit vector to the slice on which this annotation was made. For annotations made on non-oblique planes, the normal will be `[0,0,1]`.

#### `length: number`

The value of the measurement in mm.

### MeasureAngle

#### `point1, point2, vertex :` [`VoxelPoint`](export-annotation-format.md#voxelpoint-i-number-j-number-k-number)&#x20;

Angle measurement is defined by three points, where the vertex is the middle point. The angle between the two vectors (vertex -> point1 and vertex -> point2) defines the angle measurement. These points are all represented in IJK image coordinate space.&#x20;

#### `absolutePoint1, absolutePoint2 :` [`WorldPoint`](export-annotation-format.md#worldpoint-x-number-y-number-j-number)&#x20;

Corresponding to `point1`, `point2`, `vertex`, these values are coordinates in the DICOM world coordinate system i.e. physical space.&#x20;

#### `normal: [number, number, number]`

Measurements can be made on oblique planes. `normal` defines the normal unit vector to the slice on which this annotation was made. For annotations made on non-oblique planes, the normal will be `[0,0,1]`.

#### `angle: number`

The value of the angle in degrees.

## Consensus Export

When exporting consensus annotations, the Tasks JSON file and the `segmentations/` directory will have a slightly modified structure.&#x20;

### Segmentations

Each task folder will contain all the users' segmentation files. The segmentation files can be uniquely identified by the index "\_1" at the end of the file. You will be able to map between the users email and the index in `tasks.json` file.&#x20;

```
project_id/
├── segmentations
│   ├── study01
│   │   ├── series1_1.nii
│   │   └── series1_2.nii
│   └── study02
│       ├── series1_1.nii
│       └── series1_2.nii
└── tasks.json
```

### Tasks JSON

```typescript
// Single task on RedBrick can be single/multi-series
type Task = {
  // Required on upload and export
  name: string;
  consensus: true; 
  consensusScore: number; // overall consensus score
  consensusTasks: ConsensusTask[]

  // Only required on export
  taskId?: string;
  currentStageName?: string;
  createdBy?: string;
  createdAt?: string;
  updatedBy?: string;
  updatedAt?: string;
};

type ConsensusTask = {
  updatedBy: string;
  updatedAt: string; 
  scores: {secondaryUserEmail: string, score: number}[]
  series: Series[]
}
```

### The `ConsensusTask` Object

The consensus task object contains information about the consensus annotations for this task. There will be a single entry for every annotator who annotated this task. For example, if 3 users annotated each task in your project, the length of the `consensusTasks` array will be 3.

#### `updatedBy: string`

The e-mail of the user who annotated the task.

#### `updatedAt: string`

The datetime when the user last updated the task.

#### `scores: {secondaryUserEmail: string, score: number}[]`&#x20;

The `scores` entry compares the current users' annotations with every other user. The scores array will be of length n-1, where n is the number of users who annotated this task. `score` is the similarity score between the current user, and `secondaryUserEmail`.

#### `series: Series[]`

The [series entry](export-annotation-format.md#series) for the current user only.
