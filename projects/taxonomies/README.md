# Taxonomies

Taxonomies allow you to define the features you'd like to annotate in your project and apply them to your data quickly and accurately. They ensure all annotations follow a structured schema, which is automatically imported to the left hand sidebar of RedBrick AI's annotation tool.

{% embed url="https://www.loom.com/share/e8284913a9784d10a58293d707568706" %}

<figure><img src="../../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_7532ec0d-c308-4274-a68e-a88da9eaa887_tool_Label_taskid=f7cf207e-989e-4d52-9bb0-34e2549a306e (1).png" alt=""><figcaption></figcaption></figure>

### Objects

The features that you will annotate in your images are known as Objects. Objects are defined with a Label Type and Category name (e.g., "Edema" & `Segmentation)`, and RedBrick AI supports the following Object Label Types:&#x20;

| Object Label Type  | 2D Image  | 3D Image  | 2D Video |
| ------------------ | --------- | --------- | -------- |
| Segmentation       | ✅         | ✅         |          |
| Landmarks          | ✅         | ✅         | ✅        |
| Angle Measurement  | ✅         | ✅         |          |
| Length Measurement | ✅         | ✅         |          |
| Bounding Box       | ✅         | ✅         | ✅        |
| Ellipse            | ✅         | ✅         |          |
| Polygon            | ✅         |           | ✅        |
| Polyline           | ✅         |           | ✅        |

### Attributes

Attributes allow you to add a deeper level of classification to your Object Labels. Attributes are commonly used to collect more information about a particular object (e.g. "True/False" for an Object titled "tumor malignancy"). RedBrick AI offers the following Attribute Types:&#x20;

| Attribute Type | Description                                                               |
| -------------- | ------------------------------------------------------------------------- |
| Boolean        | A checkbox that can be either True or False                               |
| Select         | A dropdown that can be a single value from a list of predefined values    |
| Multi-select   | A dropdown that can have multiple values from a list of predefined values |
| Textfield      | A text input that can record free form text                               |

### Classification

Classifications can be created at the Study, Series and Instance Levels. Just like Attribute Types, Classifications can be Booleans, Selects, Multi-selects, or Textfields, and you can create multiple Classification options for your Taxonomy if necessary.

_Study-Level Classifications_ are a classification for an entire Task.&#x20;

_Series-Level Classifications_ are applied to a single series (e.g. the T1 sequence from an entire MRI study).&#x20;

_Instance-Level Classifications_ are applied to a single frame of a video and are only available for 2D video formats.

| Classification Type | 2D Image | 3D Image | 2D Video |
| ------------------- | -------- | -------- | -------- |
| Study               | ✅        | ✅        | ✅        |
| Series              | ✅        | ✅        | ✅        |
| Instance            |          |          | ✅        |

## Creating and Using Taxonomies

To create a new Taxonomy, navigate to the Taxonomy page in the left hand side bar of the RedBrick web app and click on **Create Taxonomy V2**. All taxonomies must contain at least one Object Label or Classification in order to be successfully created.&#x20;

Taxonomies are created and stored at the Organization level_._  When creating a new project, you have to select a taxonomy that you will use for the project.&#x20;

## Modifying Taxonomies

Taxonomies can be modified and saved in the **Taxonomy** page.&#x20;

{% hint style="warning" %}
Taxonomies that are being used in projects cannot be deleted
{% endhint %}

{% hint style="danger" %}
If you delete an Object Category, Attribute, or Classification from your Taxonomy, all existing associated annotations will need to be updated.
{% endhint %}

## Taxonomy V1 vs. Taxonomy V2

We released Taxonomy V2 on October 20th, 2022 with several upgrades that made taxonomies much more robust and flexible. For now, we are continuing to provide support for the legacy Taxonomy V1 as well as Taxonomy V2 to ensure that our clients won't experience any disruptions with their projects.&#x20;

We will continue to allow the creation and use of Taxonomy V1. However, we are planning to eventually deprecate support for Taxonomy V1.&#x20;

**We strongly suggest that all clients move all new projects to Taxonomy V2.**&#x20;

Some of the many improvements released with Taxonomy V2 include:&#x20;

1. The ability to pre-define an annotation type with a category, which drastically simplifies the label creation workflow;&#x20;
2. The ability to change Category names, Attribute names and Attribute options;
3. More robust support for deleting Categories and Attributes;&#x20;
4. Study-Level, Series-Level and Instance-Level classification;&#x20;

The upgrades that came along with Taxonomy V2 are not compatible with Taxonomy V1. To make use of the host of new features and improvements, create a new Taxonomy V2 and apply it to a new project.

