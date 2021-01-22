# Classification

The Classification entity is a representation for classification labels on a single datapoints. There are two sub-modules, one for each datapoint type.

### Image Classify <a id="image-classify"></a>

The `ImageClassify` module is an object representation of classification labels for a single image.

```python
redbrick.entity.label.classify.ImageClassify(remote_labels: list)
```

**Parameters**

| Parameter | Description |
| :--- | :--- |
| `remote-labels` | `remote-labels` is an object containing the labels information. The format is specified below. |

```javascript
[
  {
    "category": List[List[str]], # must match taxonomy used in the project
    "frameclassify": True
  }
]
```

### Video Classify <a id="video-classify"></a>

The `VideoClassify` module is an object representation of classification labels for a single video.

```python
redbrick.entity.label.classify.VideoClassify(remote_labels: list)
```

**Parameters**

| Parameter | Description |
| :--- | :--- |
| `remote-labels` | `remote-labels` is an object containing the labels information. The format is specified below. |

```javascript
[
  {
    "category": List[List[str]], # must match taxonomy used in the project
    "frameclassify": True,
    "frameindex": int # The frame of the video that this class is for
  },
  .
  .
  .
]
```

