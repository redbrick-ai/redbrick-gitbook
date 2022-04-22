# Annotation Format PNG Masks

{% hint style="info" %}
PNG Mask format is only supported for 2D`IMAGE_SEGMENTATION` projects&#x20;
{% endhint %}

For exporting to masks, or importing masks to RedBrick AI projects, you have to follow the formats outlined in this section. The masks directory will have the following structure:

```shell
# On Export, the directory will be named after your project_id
# On Upload, you can name the directory whatever you like. 

project_id 
├── uuid_1.png # On Export, masks file name will be the unique task_id. 
├── uuid_2.png # On Upload, mask file name will be used as the datapoint name.
├── uuid_3.png
├── datapoint_map.json # Map from mask filename -> image items path
└── class_map.json # Map from object category -> mask color
```

**PNG Masks**

The masks will be RGB PNG's with 8 bit integer pixel values `[0, 255]` (the corresponding class can be found the `class_map.json`).&#x20;

**Class Map**

The mask PNG's are 3 channel RGB images. The mapping from RGB values to category names is provided in the `class_map.json`.&#x20;

```json
// class_map.json
{
    "category_1": [1, 10, 2] // rgb values [0, 255]
    "category_2": [29, 198, 22]
    .
    .
}
```

**Datapoint Map**

The `datapoint_map.json` file contains a mapping between the mask filename and the corresponding image file path. The `datapoint_map.json` will be the following format:&#x20;

* Keys
  * Name of your PNG masks, which will be the unique `task_id` field.
* Values
  * &#x20;The [items field](../../projects/importing-data/#items-list) that was used on upload. If Direct Upload was used, this will be a string with your original filename at the end of the string for e.g. `uuid/images/uuid/your_file_name.png`.

```json
// datapoint_map.json
{
    "mask_file_name_1.png": "https://path_to_my_image_1.png", 
    "mask_file_name_2.png": "https://path_to_my_image_2.png", 
    .
    .
}
```
