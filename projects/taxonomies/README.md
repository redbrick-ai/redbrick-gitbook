# Taxonomies

Taxonomies allow you to define the features you are annotating in your project. Taxonomies ensure all annotations follow a structured schema. Taxonomies also help annotators quickly annotate data by configuring the left sidebar in the annotation tool.

{% embed url="https://www.loom.com/share/e8284913a9784d10a58293d707568706" %}

<figure><img src="../../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_7532ec0d-c308-4274-a68e-a88da9eaa887_tool_Label_taskid=f7cf207e-989e-4d52-9bb0-34e2549a306e (1).png" alt=""><figcaption></figcaption></figure>

### Objects

Objects are features you annotate in your images. Objects are defined as a Label Type and Category name, for example, Edema & `Segmentation`. RedBrick AI supports the following object label types:&#x20;

| Object Label Type  | 2D Image  | 3D Image  | 2D Video |
| ------------------ | --------- | --------- | -------- |
| Segmentation       | ✅         | ✅         |          |
| Landmarks          | ✅         | ✅         | ✅        |
| Angle Measurement  | ✅         | ✅         |          |
| Length Measurement | ✅         | ✅         |          |
| Bounding box       | ✅         |           | ✅        |
| Polygon            | ✅         |           | ✅        |
| Polyline           | ✅         |           | ✅        |

### Attributes

Attributes allow you to add a deeper level of classification to your Object Labels. Attributes are commonly used to collect more information about a particular object for example, True/False for tumor malignancy. RedBrick AI offers the following attribute types:&#x20;

| Attribute Type | Description                                                                |
| -------------- | -------------------------------------------------------------------------- |
| Boolean        | A checkbox that can be either True or False                                |
| Select         | A dropdown that can be a single value from a list of pre-defined values    |
| Multi-select   | A dropdown that can have multiple values from a list of pre-defined values |
| Textfield      | A text input that can record free form text                                |

### Classification

You can create multiple classification options in your taxonomy, and classifications can be at the Study level or at the Series Level. The different types of classifications are the same as the types of Attributes i.e. Boolean, Select, Multi-select, and Textfield.&#x20;

_Study Level Classifications_ are equivalent to a classification for the entire Task.&#x20;

_Series Level Classifications_ are applied to a single series, for example, just the T1 sequence from an entire MRI study.&#x20;

## Creating and using Taxonomies

You can create taxonomies from the Taxonomy Page (found on the application left bar) by clicking on Create Taxonomy V2. You must create at least one Object Label or Classification to create a taxonomy.&#x20;

Taxonomies are created and stored at the **Organization level**_**.**  _ When you create a project you have to select which taxonomy from your project you will use.&#x20;

## Modifying Taxonomies

To modify your taxonomy after using them in your project, please head over to the Taxonomy Page and update the taxonomy.&#x20;

{% hint style="warning" %}
Taxonomies that are being used in projects cannot be deleted
{% endhint %}

{% hint style="danger" %}
If you delete an Object Category, Attribute, or Classification from your Taxonomy, all existing associated annotations will need to be updated.
{% endhint %}

## Taxonomy V1 vs. Taxonomy V2

We released Taxonomy V2 on October 20th, 2022 with several upgrades that make taxonomies more robust and flexible. For now, we are supporting the legacy Taxonomy V1, and Taxonomy V2 to ensure there is no disruption to any projects. Some of the benefits of Taxonomy V2 over V1 are:&#x20;

1. You can pre-define the annotation type with a category. This drastically simplifies the label creation workflow.&#x20;
2. You can change category names, attribute names and attribute options.
3. There is more robust support for deleting categories and attributes.&#x20;
4. Taxonomy V2 offers study-level classification and series-level classification.&#x20;

The new upgrades with Taxonomy V2 are not compatible with Taxonomy V1. To use the new features you will have to create a new Taxonomy V2 and use it in a new project.

We will continue to allow the creation and use of Taxonomy V1, however, our plan will be to deprecate support for Taxonomy V1 in the future. **We strongly suggest you move all new projects to Taxonomy V2.**&#x20;
