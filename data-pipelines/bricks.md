# Bricks

This sections covers the details of each of the bricks you can use in RedBrick pipelines, and the possible configuration. 

## dataset-input

`dataset-input` acts as a 'source' of data for your pipeline. Get data from your dataset into a pipeline using the `dataset-input` brick.

#### Configuration

* **Dataset:** The name of the dataset that will be used as the source for this brick. 

**Accepted Inputs**

* **`NONE`**

**Accepted Outputs**

* **`image_items`**
* **`video_items`**

## labelset-input

`labelset-input` acts as a 'source' of data and labels for your pipeline. If you have data and labels in a labelset, you can bring them into your pipeline using the `labelset-input`.

**Configuration**

* **Labelset:** The name of the labelset containing data/labels that will act as the source for this brick. 

**Accepted Inputs**

* **`NONE`**

**Accepted Outputs**

* **`image_<label_type>`**
* **`video_<label_type>`**

Where `<label_type>` is the type of labels in the labelset i.e. `bbox`, `classify`, `segmentation` etc. 

## labelset-output

`labelset-output` stores your data and labels in the data warehouse. Use the `labelset-output` brick to store your generated annotations in a specified labelset.

**Configuration**

* **Labelset:** The name of the labelset that will store the data/labels.  

**Accepted Inputs**

* **`image_<label_type_code>`**
* **`video_<label_type_code>`**

Where `<label_type_code>` is a [label type code](../data-labeling/overview.md) of the labels in the labelset.

**Accepted Outputs**

Accepted outputs are the same as the inputs, and the actual output type must match the input type. 

{% hint style="warning" %}
The incoming data type, label type, and taxonomy must match the types of the labelset.
{% endhint %}

## manual-labeling

`manual-labeling` allows you to create and/or edit labels on your image and video data. 

**Configuration**  
The labeling interface for this brick will be configured using these 

* **Taxonomy:** The [taxonomy](../data-warehouse-1/taxonomies.md) of the label classes that you are generating. 
* **Label Type:** The type of labels that you wish to manually generate. The selection will be one of the[ label types](../data-labeling/overview.md).

**Accepted Inputs**

* **`image_items`**
* **`video_items`**
* **`image_<label_type_code>`**
* **`video_<label_type_code>`**

**Accepted Outputs**

* **`image_<label_type_code>`**
* **`video_<label_type_code>`**

## remote-labeling

`remote-labeling` allows you to use your own model running your own system to label data using the RedBrick Python SDK.  
  
The configuration for the `remote-labeling` brick is the same as the configuration for the `manual-labeling` brick. 

## expert-review





\*\*\*\*

