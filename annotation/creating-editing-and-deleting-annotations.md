# Creating, editing and deleting annotations

The left side bar of the annotation tool will display the Taxonomy you created. There are three sections to the side bar (that will be present depending on your taxonomy) - **Study Classification**, **Series Classification** and **Object Labels.**

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_7532ec0d-c308-4274-a68e-a88da9eaa887_tool_Label_taskid=f7cf207e-989e-4d52-9bb0-34e2549a306e (1).png" alt=""><figcaption></figcaption></figure>

## Study and Series Classification

If present, the study and series classifications will be present under their own expansion panels. You will be able to directly fill out the checkbox, select, or textfield in the grid.&#x20;

{% hint style="info" %}
Adjust the size of the grid for easy interaction
{% endhint %}

<figure><img src="../.gitbook/assets/ezgif.com-gif-maker (14).gif" alt=""><figcaption></figcaption></figure>

## Object Labels

An object label has three components - **a category name, a label type, and attributes (optional)**. The left side bar will show all the object labels on the left side bar with an option to create _instances of that object label_. All instances are organized within each object labels expansion panel.&#x20;

### Creating Object Labels

Simply click the (+) button of the object label you want to create. Doing so will create an instance of that object label, and automatically select the default tool for that label type ex. for segmentations, the brush tool will be selected by default.&#x20;

{% hint style="info" %}
Use the number shortcuts i.e. 1, 2, 3, etc., to quickly create object labels
{% endhint %}

<figure><img src="../.gitbook/assets/ezgif.com-gif-maker (15).gif" alt=""><figcaption></figcaption></figure>

### Selecting and Editing Object Labels

To edit an object label, you must first select it from the left sidebar. Once you select the instance from the left side bar, the default tool for that label type will be selected and you can interact with the canvas to make edits to that instance.&#x20;

{% hint style="info" %}
When a object label instance is selected, interacting with the canvas will only edit that particular instance.
{% endhint %}

### Other Object Labels Actions

There are several actions available that can help you with selecting, viewing, and editing object labels. All actions can be accessed by clicking the three dot menu button on a label instnance.&#x20;

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-02 at 8.41.18 AM.png" alt=""><figcaption></figcaption></figure>

#### Editing the category and attributes

You can edit the _selected labels_ attribute and category on the right side context panel. Either select the label, or click on the "Edit" label action to display the right side context panel.&#x20;

<figure><img src="../.gitbook/assets/ezgif.com-gif-maker (16).gif" alt=""><figcaption></figcaption></figure>

#### Deleting Object Labels

You can delete the _selected object label_ by using the `delete` / `backspace` shortcut. Alternatively, you can use the delete action in the actions dropdown.&#x20;

To delete all labels use the shortcut `shift + delete`/`shift + backspace`. Alternatively, you can use the delete all action in the _Object Labels_ three dot menu dropdown.&#x20;

#### Hide and Show Labels

You can hide the _label you are currently hovering over_ by using the `h` hotkey. If you are not hovering over any label (either on the canvas, or on the left side bar), the `h` hotkey will hide/show the currently selected label.&#x20;

To hide/show all labels use the shortcut `shift + h` or the hide all action in the _Object Labels_ three dot menu dropdown.&#x20;

#### Lock and Unlock Labels

You can lock/unlock _label you are currently hovering over_ by using the `u` hotkey. If you are not hovering over any label (either on the canvas, or on the left side bar), the `u` hotkey will lock/unlock the currently selected label.

To lock/unlock all labels use the shortcut `shift + u` or the lock all action in the _Object Labels_ three dot menu dropdown.&#x20;

Watch the video below to understand how to prevent/allow overwriting of annotations.

{% embed url="https://www.loom.com/share/7daf374f6967429dad43b2962c6ccd8f" %}

#### Toggle Vibrant Mode

Vibrant mode allows you to temporarily highlight a particular instance. For example, if you have several small instances of nodules in a chest CT, you can hover over any particular instance on the left side bar or on the canvas, and use the `v` shortcut to activate vibrant mode to highlight that instance. This can be useful in quickly identifying instances.&#x20;

#### Jump to Label

The Jump to label action will change the current slice position to the closest slice position that contains a particular annotation. This is useful for revealing annotations on the canvas.&#x20;
