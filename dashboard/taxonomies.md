# Taxonomies

Taxonomies allow you to define the structures that you'd like to annotate in your project and apply them to your data quickly and accurately. They ensure all annotations follow a structured schema which is automatically imported to the left hand sidebar of RedBrick AI's Annotation Tool.

<figure><img src="../../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_7532ec0d-c308-4274-a68e-a88da9eaa887_tool_Label_taskid=f7cf207e-989e-4d52-9bb0-34e2549a306e (1).png" alt=""><figcaption></figcaption></figure>

### Object Label Types

Object Labels are the structures that your team will annotate on RedBrick AI.&#x20;

When creating your Taxonomy, you must define a Label **Type** (e.g. "Segmentation") and a **Name** (e.g. "Edema") for each Object Label.

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

RedBrick AI supports the following Object Label Types:&#x20;

<table><thead><tr><th width="220">Object Label Type</th><th>2D Image </th><th>3D Image </th><th>2D Video</th></tr></thead><tbody><tr><td>Segmentation</td><td>✅</td><td>✅</td><td></td></tr><tr><td>Landmarks</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Angle Measurement</td><td>✅</td><td>✅</td><td></td></tr><tr><td>Length Measurement</td><td>✅</td><td>✅</td><td></td></tr><tr><td>Bounding Box</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Ellipse</td><td>✅</td><td>✅</td><td></td></tr><tr><td>Polygon</td><td>✅</td><td></td><td>✅</td></tr><tr><td>Polyline</td><td>✅</td><td></td><td>✅</td></tr><tr><td>Cuboid</td><td></td><td>✅</td><td></td></tr></tbody></table>

### Object Label Attributes

Attributes allow you to add a deeper level of classification to your Object Labels. Attributes are commonly used to collect more information about a particular object (e.g. "True/False" for an Object titled "tumor malignancy"). RedBrick AI offers the following Attribute Types:&#x20;

<table><thead><tr><th width="213">Attribute Type</th><th>Description</th></tr></thead><tbody><tr><td>Boolean</td><td>A checkbox that can be either True or False</td></tr><tr><td>Select</td><td>A dropdown that can be a single value from a list of predefined values</td></tr><tr><td>Multi-select</td><td>A dropdown that can have multiple values from a list of predefined values</td></tr><tr><td>Textfield</td><td>A text input that can record free form text</td></tr></tbody></table>

### Classifications

Classifications are data attributes that can be affixed to studies, individual Series, or individual video frames.

Just like Object Label Attributes, Classifications can be **Booleans**, **Single Selects**, **Multi-selects**, or **Text** fields, and there is no limit to the number of Classifications you can have in your Taxonomy.

_**Study-Level Classifications**_ are a classification for an entire Task (e.g. an MRI study consisting of 4 Series).

_**Series-Level Classifications**_ are applied to a single series (e.g. the T1 sequence from an MRI study).&#x20;

_**Instance-Level Classifications**_ are applied to a single frame of a video and are only available for 2D video formats.

<table><thead><tr><th width="238">Classification Type</th><th width="168">2D Image</th><th width="169">3D Image</th><th>2D Video</th></tr></thead><tbody><tr><td>Study</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Series</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Instance</td><td></td><td></td><td>✅</td></tr></tbody></table>

## Creating Taxonomies

Taxonomies are created and stored at the Organization level, which allows you to use a single Taxonomy for several Project&#x73;_._ &#x20;

To create a new Taxonomy in the UI, navigate to the **Taxonomies** page in the left hand side bar of the RedBrick web app and click on **Create Taxonomy**.&#x20;

Taxonomies can also be created using the [`create_taxonomy()` SDK method](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.organization.RBOrganization.create_taxonomy).

{% hint style="success" %}
All Taxonomies must contain at least one Object Label or Classification in order to be successfully created.&#x20;
{% endhint %}

## Modifying Taxonomies

Taxonomies can be modified on the **Taxonomies** page of the UI at any time.

Alternatively, you can use the [`update_taxonomy()` SDK method](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.organization.RBOrganization.update_taxonomy) to modify a Taxonomy outside of the UI. Please note the following about modifying existing Taxonomies:

1. the `update_taxonomy()` method overwrites the current Taxonomy in its entirety;
2. If you delete an Object Category, Attribute, or Classification from your Taxonomy, all existing associated annotations will need to be updated;
3. Taxonomies that are being used in Projects cannot be deleted;

## Duplicating a Taxonomy

There are two ways to duplicate an existing Taxonomy in RedBrick's UI:

1. On the Taxonomies page, open the three-dot menu of the Taxonomy you'd like to duplicate and click on **Duplicate Taxonomy**.
2. Within the Taxonomy you'd like to duplicate, open the three-dot menu in the top-right corner of the screen and click on **Duplicate Taxonomy**.

You'll then be directed to provide a name for the newly duplicated Taxonomy. Input a unique name, click on **Create Taxonomy**, and you have successfully created a duplicate!

<figure><img src="../../.gitbook/assets/copying-taxonomies.gif" alt=""><figcaption><p>Walkthrough of Taxonomy duplication</p></figcaption></figure>

{% hint style="info" %}
**SDK Mastery:** when duplicating a Taxonomy, the archived elements of the Source Taxonomy are not transferred to the Duplicate Taxonomy.&#x20;

Be sure to validate your [objectTypes](https://sdk.redbrickai.com/formats/taxonomy.html#redbrick.types.taxonomy.ObjectType) in the Duplicate Taxonomy, as values may have changed!
{% endhint %}

## Nesting Taxonomy Elements

Taxonomies now support the nesting of Object Labels, Study-Level and Series-Level Classifications both in the UI and via the RedBrick AI Python SDK.&#x20;

By adding the parents attribute to your Taxonomy, you can create and/or designate Parent Tiers for a given Object Label.

{% embed url="https://www.loom.com/share/7c292d311c02490392e83b77319a4040" %}
Nested Object Labels in the Annotation Tool
{% endembed %}

### Nesting Object Labels in the UI

In the Taxonomies page, simply click on **Add Folder** and give your folder a name.

You can then easily drag and drop your Objects Labels or Classifications into your folder.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Nesting Object Labels via SDK

You can create Parent Tiers by adding the `parents:[]` attribute to any Object Label, Study-Level, Series-Level, or Instance-Level Classification within your Taxonomy. Parent Tiers are created and assigned from **left to right and in descending order**, which means the first string in `parents:[]` will always be a Tier 1 Parent, the second string will be a Tier 2 Parent, and so on.

For full documentation, please see our [Taxonomy Object reference](../../python-sdk/formats/full-format-reference.md#taxonomy-object).

For an example of a two-tiered Object Label structure, please see the example code below:

```python
org.create_taxonomy_new(
    "Clinical Study 1",
        
    object_types=
    [
        {
            "category": "Herniated Disc",
            "labelType": "SEGMENTATION",
            "attributes": [],
            "color": "#7FFFD4",
            "classId": 0,
            # Creates the Tier 1 Parent 'Spine Pathologies' and Tier 2 Parent 'Disc Pathologies'
            "parents": ['Spine Pathologies', 'Disc Pathologies'],
        },
        {
            "category": "Bulging Disc",
            "labelType": "SEGMENTATION",
            "attributes": [],
            "color": "#DEB887",
            "classId": 1,
            "parents": ['Spine Pathologies', 'Disc Pathologies'],
        },
        {
            "category": "Degenerated Disc",
            "labelType": "SEGMENTATION",
            "attributes": [],
            "color": "#00FFFF",
            "classId": 2,
            "parents": ['Spine Pathologies', 'Disc Pathologies'],
        },
        {
            "category": "Vertebral Fracture",
            "labelType": "SEGMENTATION",
            "attributes": [],
            "color": "#FF7F50",
            "classId": 3,
            "parents": ['Spine Pathologies'],
        },
    ],
)
```

The above Taxonomy will be nested in the Annotation Tool as well. Tiers can also be collapsed or expanded as necessary, allowing you to easily navigate through Label Tiers and save screen space.

## HTML Tooltips

RedBrick AI allows users to attach custom HTML tooltips to any Object Label, Study-Level Classification, Series-Level, or Instance-Level Classification. For larger, more complex Taxonomies, these tooltips can be a great form of input for annotators or serve as a record for any internal standards that may be associated with the annotation itself.

### Creating HTML Tooltips in the UI

First, open a Taxonomy and click on any Object Label or Classification. The Hint field will then appear, allowing you to copy/paste your HTML into RedBrick or write your own using our intelligent autocomplete feature.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="563"><figcaption><p>Creating an HTML tooltip in the UI</p></figcaption></figure>

### Creating HTML Tooltips via SDK

If you're prefer to create HTML Tooltips with the SDK, you can use the `hint: string` attribute to insert a string of HTML that will display in a tooltip next to an annotation upon hover. Please see the following code for an example of an Object Label with an HTML tooltip.

```python
object_types=
    [
        {
           "category": "Herniated Disc",
           "labelType": "SEGMENTATION",
           "attributes": [],
           "color": "#7FFFD4",
           "classId": 0,
           "parents": ['Spine Pathologies', 'Disc Pathologies'],
           "hint": '<h2>Annotate each instance separately!</h2><a href=https://en.wikipedia.org/wiki/Spinal_disc_herniation>Reference</a><p>Send qs to Jason</p>'
         },
]
```

{% hint style="info" %}
All HTML elements can be included within the `hint: string` attribute, but images must be inserted using `<img src>` and a relevant link.
{% endhint %}

The above code displays as follows in the Annotation Tool:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-23 at 12.32.17.png" alt=""><figcaption><p>The HTML Tooltip that appears while hovering your cursor over the "?" icon</p></figcaption></figure>

{% hint style="warning" %}
For security reasons, we do not allow scripts to be executed within HTML Tooltips.
{% endhint %}
