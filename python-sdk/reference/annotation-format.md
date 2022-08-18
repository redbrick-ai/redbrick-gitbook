# Annotation Format

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

## Segmentations

The segmentation directory will contain a single sub-directory for each task in your export. The sub-directories will be named after the task [`name`](annotation-format.md#name-string). A single task (depending on whether it was single series or multi-series) can have one or more segmentations.

The individual segmentation files will be in NIfTI-1 format and be [named after the user-defined series name](annotation-format.md#name-string-1). If no series name is provided on upload, RedBrick will assign a unique name. Corresponding meta-data ex. category names will be provided in [tasks.json](annotation-format.md#tasks-json).

## Tasks JSON

There will be a **single entry for each task** in the items file. Please see the definition (typescript) of the JSON object below:

```typescript
type Tasks = Task[];

// Single task on RedBrick can be single/multi-series
type Task = {
  // Required on upload and export
  name: string;
  series: Series[];
  segmentMap?: { [instanceId: number]: { category: string | string[] } };

  // Only required on export
  taskId?: string;
  currentStageName?: string;
  createdBy?: string;
  createdAt?: string;
  updatedBy?: string;
  updatedAt?: string;
};

// A single series can be 2D, 3D, video etc.
type Series = {
  items: string | string[];
  name?: string;

  segmentations?: string | string[];
  segmentMap?: { [instanceId: number]: { category: string | string[] } };
  landmarks3d?: Landmarks3D[];
  measurements?: (MeasureLength | MeasureAngle)[];
  boundingBoxes?: BoundingBox[];
  polygons?: Polygon[];
  polylines?: Polyline[];
  classifications?: Classification[];
};

// Label Types
type Landmarks3D = {
  x: number;
  y: number;
  z: number;
  category: string | string[];
  attributes: Attributes;
};

type MeasureLength = {
  type: 'length';
  point1: [number, number, number];
  point2: [number, number, number];
  absolutePoint1: [number, number, number];
  absolutePoint2: [number, number, number];
  normal: [number, number, number];
  length: number;
  category: string | string[];
  attributes: Attributes;
};

type MeasureAngle = {
  type: 'angle';
  point1: [number, number, number];
  point2: [number, number, number];
  vertex: [number, number, number];
  absolutePoint1: [number, number, number];
  absolutePoint2: [number, number, number];
  absoluteVertex: [number, number, number];
  normal: [number, number, number];
  angle: number;
  category: string | string[];
  attributes: Attributes;
};

type BoundingBox = {
  x: number;
  y: number;
  width: number;
  height: number;
  category: string | string[];
  attributes: Attributes;

  // video meta-data
  frameIndex: number;
  trackId: string;
  keyFrame: number;
  endTrack: Boolean;
};

type Polygon = {
  points: { x: number; y: number }[];
  category: string | string[];
  attributes: Attributes;

  // video meta-data
  frameIndex: number;
  trackId: string;
  keyFrame: number;
  endTrack: Boolean;
};

type Polyline = {
  points: { x: number; y: number }[];
  category: string | string[];
  attributes: Attributes;

  // video meta-data
  frameIndex: number;
  trackId: string;
  keyFrame: number;
  endTrack: Boolean;
};

type Classification = {
  category: string | string[];

  // video meta-data
  frameIndex: number;
  trackId: string;
  keyFrame: number;
  endTrack: Boolean;
};

type Attributes = {
  [attributeName: string]: string | boolean;
};
```

### Task

The `Task` object represents a single task on RedBrick AI. It contains task-level meta-data information about all the series within the task. A task can contain a [single series or multiple series](../../dicom-annotation/layout-series-study.md) (ex. a full MRI study).&#x20;

#### `name: string`

A user-defined string is defined on upload. Exported data will include this value. `name` is meant to be a human-readable string that can help identify tasks ex. you can set `name` of a task to `patient/study01`.

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

#### `segmentMap?: {[instanceId: number]: { category: string | string[] }}`

A mapping between segmentation instance id, and your taxonomy category name.`segmentMap` can be defined either at the task level or [at the series level](annotation-format.md#segmentmap-instanceid-number-category-string-or-string-1). When defined at the task-level, the mapping will apply annotations in all the series - this is useful for semantic segmentation applications.

### Series

The `Series` object has meta-data and annotations for a single series within a task. A series can represent a single MRI/CT series, a video or a single 2D image. If a series has annotations, you can expect one or more of the label entries to be present i.e. `segmentations`, `polygons` etc.

#### `items: string | string[]`

The items entry is a list of file paths that point to your data. Please have a look at the [#items-list](../../importing-data/import-cloud-data.md#items-list "mention")documentation to understand how to format for various modalities and series/study uploads.

#### `name?: string`

An optional user-defined string. Individual [series will be named after this value on the labeling tool](https://www.loom.com/i/ea12e486bd8845d7b3b8a83fc115ad58). Exported segmentation files will also be named using this value. Using the Series Instance UID here is good practice. &#x20;

### Common Label Keys

Here are the definition for some common entries present in some/all label entries.&#x20;

#### `category: string | string[]`

The class of your annotations. This value is part of your [project taxonomy](../../projects/taxonomies.md). If the class is nested, `category` will be `string[]`.

#### `attributes: {[attributeName: string]: string | boolean}`

Each annotation can have accompanying attributes, that are also defined in your [project taxonomy](../../projects/taxonomies.md). `attributeName` is defined when creating your taxonomy.&#x20;

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

#### `segmentMap?: {[instanceId: number]: { category: string | string[] }}`

A mapping between segmentation instance id, and your taxonomy category name.`segmentMap` can be defined either at the [task level](annotation-format.md#segmentmap-instanceid-number-category-string-or-string) or at the series level. When defined at the series-level, the mapping will apply only to the current series, and instance ids must be unique across all series in a task - this is useful for instance segmentation.&#x20;

### Landmarks3D

#### `x:number, y:number, z:number`

Coordinates of the point in three-dimensional space. These values are in the IJK coordinate space i.e. with respect to the 3D image, z is the slice number and x, y are equivalent to indexing the 3D image by row, column. &#x20;

### Polygon

#### `points: { x: number; y: number }[]`

A list of x,y points in IJK image coordinate space. The array is ordered such that each point is connected to the next point in the array. The first and last points are also connected.&#x20;

### Polyline

#### `points: { x: number; y: number }[]`

A list of x,y points in IJK image coordinate space. The array is ordered such that each point is connected to the next point in the array.

### MeasureLength

#### `point1, point2 : [number, number, number]`&#x20;

A length measurement is defined by two points. Each point is defined by 3 numbers representing x,y,z coordinates in IJK image coordinate space.

#### `absolutePoint1, absolutePoint2 : [number, number, number]`&#x20;

Corresponding to `point1`, `point2` these values are coordinates in the DICOM world coordinate system i.e. physical space.&#x20;

#### `normal: [number, number, number]`

Measurements can be made on oblique planes. `normal` defines the normal unit vector to the slice on which this annotation was made. For annotations made on non-oblique planes, the normal will be `[0,0,1]`.

#### `length: number`

The value of the measurement in mm.

### MeasureAngle

#### `point1, point2, vertex : [number, number, number]`&#x20;

Angle measurement is defined by three points, where the vertex is the middle point. The angle between the two vectors (vertex -> point1 and vertex -> point2) defines the angle measurement. These points are all represented in IJK image coordinate space.&#x20;

#### `absolutePoint1, absolutePoint2 : [number, number, number]`&#x20;

Corresponding to `point1`, `point2`, `vertex`, these values are coordinates in the DICOM world coordinate system i.e. physical space.&#x20;

#### `normal: [number, number, number]`

Measurements can be made on oblique planes. `normal` defines the normal unit vector to the slice on which this annotation was made. For annotations made on non-oblique planes, the normal will be `[0,0,1]`.

#### `angle: number`

The value of the angle in degrees.

## Consensus Export

When exporting consensus annotations, the Tasks JSON file and the `segmentations/` directory will have a slightly modified structure.&#x20;

### Segmentations

Each task folder will contain all the users' segmentation files. The segmentation files can be uniquely identified by the index "\_1" at the end of the file. You will be able to map between the users email and the index in [tasks.json](annotation-format.md#undefined).&#x20;

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

### ConsensusTask

The consensus task object contains information about the consensus annotations for this task. `` There will be a single entry for every annotator who annotated this task. For example, if 3 users annotated each task in your project, the length of the `consensusTasks` array will be 3.

#### `updatedBy: string`

The e-mail of the user who annotated the task.

#### `updatedAt: string`

The datetime when the user last updated the task.

#### `scores: {secondaryUserEmail: string, score: number}[]`&#x20;

The `scores` entry compares the current users' annotations with every other user. The scores array will be of length n-1, where n is the number of users who annotated this task. `score` is the similarity score between the current user, and `secondaryUserEmail`.

#### `series: Series[]`

The [series entry](annotation-format.md#series) for the current user only.
