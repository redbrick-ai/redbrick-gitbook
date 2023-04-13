---
description: Write a script to dynamically arrange the viewports for your project
---

# Custom Hanging Protocol

The Custom Hanging Protocol feature allows you to write a script that will programmatically define the annotation tool layout. This can save an annotator's time by pre-configuring the interface and layout in the desired way.

The script takes as input the available series for a particular task and returns the layout dimensions and list of views to display.

{% embed url="https://www.loom.com/share/a5b5255cd1954bd590849a8e939c9b5f" %}

## Writing Your Own Script

At present, you can control the following things:&#x20;

* The dimensions of the layout (`setDimensions`)
* The contents of each viewport in the layout (`setViews`):
  * REQUIRED: Which series to show (`seriesIndex`)
  * REQUIRED: Which way to view the series (`plane`)
  * Flip the view horizontally (`flippedHorizontally`)
  * Flip the view vertically (`flipperVertically`)
  * Activate intellisync (`synchronized`)
  * If the view is maximimized (`expanded`)
* The default windowing setting for each series (`setWindowing`)
* The default threshold setting for each series (`setThresholding`)
* The default configuration settings for the Annotation Tool (`setSegmentationSettings`)

### Types

```typescript
function setViews(views: View[]) {
 //...
}
function setDimensions(numColumns: number, numRows: number) {
 // ...
}
function setWindowing(seriesIndex: number, level: number, width: number){
 // ...
}
function setThresholding(seriesIndex: number, min: number, max: number) {
 // ...
}

function setSegmentationSettings(
  [  
    { 
      toolName: ToolOptions; 
      enabled: boolean;
      modes?: ToolModes[];
      defaultMode?: ToolModes;
      defaultTool?: boolean;
    }
  ]
);

interface Series {
  seriesIndex: number;
  is2DImage: boolean;
  isVideo: boolean;
  numFrames: number;
  name: string; // User defined name if available, else "A", "B", ...
  imagingAxis: 'AXIAL' | 'SAGITTAL' | 'CORONAL';
}

interface View {
  plane: 'AXIAL' | 'SAGITTAL' | 'CORONAL' | '3D' | 'MIP';
  seriesIndex: number;
  flippedHorizontally?: boolean;
  flippedVertically?: boolean;
  synchronized?: boolean;
  expanded?: boolean; // Only applicable to 1 view
}
```

## Examples

#### Default Script

This default script uses some defined macros to make setting the view easier.&#x20;

```typescript
function hangingProtocol(allSeries: Series[]) {
  // This is the default layout script
  if (allSeries.length > 1) {
    setMultiSeries();
  } else if (allSeries[0].is2DImage) {
    setSingleView();
  } else {
    setMPR();
  }
}
```

#### Set Single View

```javascript
function setSingleView(seriesIndex=0) {
  setDimensions(1,1);
  setViews([
    {
      plane: allSeries[seriesIndex].imagingAxis,
      seriesIndex: seriesIndex,
    }
  ]);
}
```

#### Set Multi Series Layout

This layout is for setting each series in a study as a single viewport where it is being viewed in the imaging axis.

```javascript
function setMultiSeries() {
  function singleSeries(series_, index) {
    return {
      plane: series_.imagingAxis,
      seriesIndex: index,
    };
  }
  let views = allSeries.map(singleSeries);

  setViews(views.slice(0,9));
}
```

#### Set Multi Planar Reconstruction

```javascript
function setMPR(seriesIndex=0) {
  let targetSeries = allSeries[seriesIndex];
  setDimensions(2,2);
  setViews([
    {
      plane: 'SAGITTAL',
      seriesIndex: seriesIndex,
      expanded: targetSeries.imagingAxis === 'SAGITTAL',
    },
    {
      plane: 'CORONAL',
      seriesIndex: seriesIndex,
      expanded: targetSeries.imagingAxis === 'CORONAL',
    },
    {
      plane: 'AXIAL',
      seriesIndex: seriesIndex,
      expanded: targetSeries.imagingAxis === 'AXIAL',
    },
    {
      plane: '3D',
      seriesIndex: seriesIndex,
    }
  ]);
}
```

### Synchronize Views

Hanging protocols can be used along side [intellisync.md](intellisync.md "mention")for ease of use when annotating scans in a study. This example is useful for a project where each task has 4 series from an MRI study: T1, T1CE, T2, and Flair weighted MR scans.

Sample input data:

```javascript
[
    {
        seriesIndex: 0,
        is2DImage: false,
        isVideo: false,
        numFrames: 1,
        name: 'T1',
        imagingAxis: 'SAGITTAL',    
    },
    {
        seriesIndex: 1,
        is2DImage: false,
        isVideo: false,
        numFrames: 1,
        name: 'T2',
        imagingAxis: 'SAGITTAL',    
    },
    {
        seriesIndex: 2,
        is2DImage: false,
        isVideo: false,
        numFrames: 1,
        name: 'T1CE',
        imagingAxis: 'SAGITTAL',    
    },
    {
        seriesIndex: 3,
        is2DImage: false,
        isVideo: false,
        numFrames: 1,
        name: 'Flair',
        imagingAxis: 'SAGITTAL',    
    },
]
```

Sample script to sort the views, then display the imaging axis and activate Intellisync.

```javascript
// sort series by Name
let priorities = ['t1', 't1ce', 't2', 'flair'];
allSeries.sort((a, b)=>priorities.indexOf(a.name.toLowerCase()) - priorities.indexOf(b.name.toLowerCase()));

let imagingAxis = allSeries[0].imagingAxis;

// Filter out views that were imaged in a different axis
let eligibleSeries = allSeries.filter((series) => series.imagingAxis === imagingAxis);

// Describe viewports
setViews(eligibleSeries.map((series) => {
  return {
    seriesIndex: series.seriesIndex,
    plane: series.imagingAxis,
    synchronized: true,
  };
}));
```

## Tool Configuration

The Annotation Tool can be configured using Hanging Protocols to set a default Tool, enable/disable tools, and enable/disable 2D and 3D modes.

### Default Configuration

```javascript
{
 toolName: 'brush',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
 defaultTool: true,
},
{
 toolName: 'pen',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
},
{
 toolName: 'fillHoles',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
},
{
 toolName: 'connectedThreshold',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
},
{
 toolName: 'contour',
 enabled: true,
 modes: ['3d'],
 defaultMode: '3d',
},
{
 toolName: 'islandRemoval',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
},
{
 toolName: 'paintBucket',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
},
{
 toolName: 'merge',
 enabled: true,
 modes: ['2d', '3d'],
 defaultMode: '2d',
},
```

Example Script:

```javascript
setSegmentationSettings(
 [
  // disable the Brush Tool entirely within the Editor
  {
   toolName: 'brush',
   enabled: false,
   modes: ['2d', '3d'],
   defaultMode: '2d',
  },
  // set the 2D Pen Tool as the default Annotation Tool
  {
   toolName: 'pen',
   enabled: true,
   modes: ['2d', '3d'],
   defaultMode: '2d',
   defaultTool: true,
  },
  // disable 2D Hole Filling
  {
   toolName: 'fillHoles',
   enabled: true,
   modes: ['3d'],
   defaultMode: '3d',
  },
 ]
);
  
```
