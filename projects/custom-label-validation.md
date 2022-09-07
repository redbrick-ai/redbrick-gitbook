# Custom Label Validation

You can define a custom Javascript script that can continuously compare annotations to a schema/set of rules and inform annotators (in real-time) of any mistakes in their annotations. You can also prevent annotators from submitting tasks when your validation script finds errors.

For most annotation projects, there is a schema/rule-set/taxonomy that annotators must follow. A large portion of errors in annotation projects is due to oversights/slips during labeling in adhering to the schema. \
\
For example, the annotator must segment a tumor and fill out a few related attributes if a tumor is found. A common error can be forgetting to fill out all attributes when the tumor is present. Post-processing scripts usually reveal these errors.&#x20;

Prevent simple, recurrent errors from occurring by writing a set of tests that will be run regularly, informing annotators of any mistakes they're making.

{% embed url="https://www.loom.com/share/9ae2535b823247eea128dbd2f24503e5" %}
Overview of custom label validation
{% endembed %}

## Overview

By default, all projects have a custom check to warn annotators when they submit tasks without any annotations. You can enable/disable custom validation under Project Settings -> Label Validation.&#x20;

<figure><img src="../.gitbook/assets/qa.redbrickdevteam.com_943c97cd-58b1-4794-84d0-8b00d26f0c84_projects_b4b15a0e-f26d-4f8b-80a5-4c39c6a38aac_settings (1).png" alt=""><figcaption><p>Custom label validation in settings</p></figcaption></figure>

### Prevent submissions with errors

By default, annotators will just receive the error messages as a warning, and they will still be able to submit the task anyway. To prevent the annotators from submitting with any errors present, toggle the _Prevent submission with errors_ switch.

<div>

<figure><img src="../.gitbook/assets/qa.redbrickdevteam.com_943c97cd-58b1-4794-84d0-8b00d26f0c84_projects_b4b15a0e-f26d-4f8b-80a5-4c39c6a38aac_tool_Label.png" alt=""><figcaption><p>Submission allowed</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/qa.redbrickdevteam.com_943c97cd-58b1-4794-84d0-8b00d26f0c84_projects_b4b15a0e-f26d-4f8b-80a5-4c39c6a38aac_tool_Label_taskid=4d88355c-b83c-4901-bbd1-9fd45a72d6c0.png" alt=""><figcaption><p>Submission with errors prevented</p></figcaption></figure>

</div>

### Custom Javascript function

You will write the custom validation as a Javascript function. This Javascript function will run on each annotator's browser while they are annotating data. \
\
The Javascript function has the following definition:&#x20;

```typescript
function(labels: Label[]): string[] {
  // Your custom validation logic
}
```

#### `label: Label[]`

The validation function has a single input - a list of labels containing minimal meta-data about the labels. Please see the definition of the `Label` object below:&#x20;

```typescript
interface Label {
  category: string[];
  attributes: LabelAttribute[];
  labelType: TaskType;
  numFramesLabeled?: number;
}

// Label attribute
interface LabelAttribute {
  name: string;
  value: boolean | number | string;
}

// Task Type
enum TaskType {
  ITEMS = 'ITEMS',
  CLASSIFY = 'CLASSIFY',
  BBOX = 'BBOX',
  POLYGON = 'POLYGON',
  POLYLINE = 'POLYLINE',
  POINT = 'POINT',
  ELLIPSE = 'ELLIPSE',
  SEGMENTATION = 'SEGMENTATION',
  MULTI = 'MULTI',
  MULTICLASSIFY = 'MULTICLASSIFY',
  LENGTH = 'LENGTH',
  ANGLE = 'ANGLE',
}
```

You can generate a sample `Label[]` object by going to the labeling tool -> opening command bar `cmd/ctrl + k` -> _Copy current label state to clipboard._

{% embed url="https://www.loom.com/share/90aa36c4bad44069adeac75a5765589c" %}

#### Returns `string[]`

Your custom validation script must return a list of warning/error messages describing the issues found. Return an empty array `[]` if no errors are found. These error message strings will be displayed to the annotators on the labeling tool.&#x20;

To help you write a validation function with several checks, RedBrick AI has a custom-defined function `assert` that accepts a boolean statement and a corresponding error message. The two scripts below will produce the same result:&#x20;

{% tabs %}
{% tab title="With assert()" %}
<pre class="language-typescript"><code class="lang-typescript"><strong>function(labels: Label[]): string[] {
</strong>    assert(labels.length > 1, "You have not created any labels!")
    assert(labels.length &#x3C; 5, "You have created too many labels!")
}</code></pre>
{% endtab %}

{% tab title="Without assert()" %}
```typescript
function(labels: Label[]): string[] {
    const errors: string = []
    
    if (labels.length > 1) {
        errors.push("You have not created any labels!")
    }
    if (labels.length < 5) {
        errors.push("You have created too many labels!")
    }
    
    return errors
}
```
{% endtab %}
{% endtabs %}

## Validate your code

Before saving your script, you should validate that your code executes as expected. Click on the validate button on the bottom right of the Settings page, and paste the JSON object copied from the labeling tool to see if your code executes as expected:

<figure><img src="../.gitbook/assets/Screen Shot 2022-09-04 at 3.22.20 PM.png" alt=""><figcaption></figcaption></figure>

## Displaying the validation on the labeling tool

Your custom validation script will be regularly run. If any warnings are found, an indicator will appear on the right side of the bottom bar. If you have enabled _Prevent submissions with errors_ the indicator will be red.&#x20;

<figure><img src="../.gitbook/assets/qa.redbrickdevteam.com_943c97cd-58b1-4794-84d0-8b00d26f0c84_projects_64e8b5d9-81d3-4401-a49a-924d72916b0f_tool_Label_taskid=bd8aa035-e0fa-4388-ae66-6f12c7fe2a4c.png" alt=""><figcaption><p>Submission with errors is allowed</p></figcaption></figure>

<figure><img src="../.gitbook/assets/qa.redbrickdevteam.com_943c97cd-58b1-4794-84d0-8b00d26f0c84_projects_64e8b5d9-81d3-4401-a49a-924d72916b0f_tool_Label_taskid=bd8aa035-e0fa-4388-ae66-6f12c7fe2a4c (1) (3).png" alt=""><figcaption><p>Submission with errors is prevented</p></figcaption></figure>

## Example Scripts

### Check if exact categories are present

For this example, let's say we are expecting each task to contain the following segmentations - _necrosis, enhancing tumor, non-enhacing tumor and edema._&#x20;

```typescript
function(labels: Label[]): string[] {
  const expectedCategories = [
    'necrosis',
    'enhancing tumor',
    'non-enhancing tumor',
    'edema',
  ];

  // Iterate over all expected categories
  for (const category of expectedCategories) {
  
    // Check if the category is present in any label
    const categoryPresent = labels.some(
      (label) => label.category[0] === category
    );
    
    // assert with message
    assert(categoryPresent, `The ${category} category is missing!`);
  }
}
```

### Validate only single instance of a category has been created

This script validates only a single instance of a particular category has been created. If you're expecting semantic segmentation labels, this check can ensure annotators don't accidentally create multiple instance segmentations.

```typescript
function(labels: Label[]): string[] {  
  const semanticCategory = 'edema';

  const labelsFiltered = labels.filter((label) => label.category[0] === semanticCategory);

  assert(
    labelsFiltered.length === 1,
    `Expected exactly 1 ${semanticCategory} annotation`
  );
}
```
