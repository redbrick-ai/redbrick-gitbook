# Creating, editing and deleting annotations

On RedBrick AI you can perform the following types of annotations:

1. **Segmentation** - Instance, semantic and overlapping.
2. **Classification** - Task level classifications (equivalent to series/study level annotations). To perform task level classifications, you have to add task classification categories to your [taxonomy](broken-reference).&#x20;
3. **Vector annotations** - Landmarks, and more coming soon.

## Creating annotations

When the annotation tool first loads, it will have the 'cross-hairs' tool selected. To create an annotation:

1. **Select the type of annotation** from the drop down on the **Create Label button** on the left side bar.
2. Click on **Create Label** to add an annotation. This will open the **category selection panel**, where you can choose the category and attributes for your annotation. To create **multiple instances** of the same category, simply create multiple labels with the same category selection.
3. Once the annotation is created, you will see a new entry to the annotation list on the left side bar. You will also see a list of **annotation tools appear on the top bar** e.g. brush, pen etc. The settings for your selected annotation tool will be in the **context panel** on the right.&#x20;

{% embed url="https://www.loom.com/share/8b4682acc3f4421ab4b10f2a92f7552c" %}
Creating a segmentation annotation
{% endembed %}

## Selecting and editing annotations

To modify, delete, hide, lock etc. existing annotations, you have to first **select** the annotation:

1. You can select existing annotations in two ways:&#x20;
   1. Select the annotation from the left side bar by clicking on the annotation item in the list.&#x20;
   2. Choose the **Select tool** from the top bar (or press ESC), and hover and click on any annotation on the main canvas.&#x20;
2. After selecting the annotation, the relevant annotation tools will re-appear on the top bar. You can now directly interact with the main canvas to modify the segmentation.&#x20;
3. To **change a selected annotations category** or **attributes**, you can click on the annotation item _again_ (first click selects, second click opens edit panel) to re-select the annotation/attributes. You can also **open the edit panel** by clicking on the **three dot menu** on the annotation.
4. To de-select all annotations, use the ESC keyboard shortcut, or choose the Select tool on the top bar.

{% hint style="warning" %}
You can only edit currently selected annotations. When one annotation is selected, you will not be able to make modifications to any other annotation.
{% endhint %}

{% hint style="info" %}
Tips

1. While an annotation is selected, use the `E` keyboard shortcut to open the edit panel
2. To bring a selected annotation into view, use the SHIFT + J keyboard shortcut
3. If an annotation has attributes associated with it, you can get a summary view by hovering over the attribute number indicator.
{% endhint %}

{% embed url="https://www.loom.com/share/7e49c1375a0444db9382ca04d44656a9" %}
Modifying an existing annotation
{% endembed %}

## Lock, hide, and delete

### Lock/un-lock

While making annotations you may want to lock a specific annotation to make sure you don't accidentally edit / overwrite it while making other segmentations. You can lock/un-lock any annotation from the **three dot drop down menu**.

Alternatively, you can hover over an annotation/select an annotation and use the `U` keyboard shortcut.&#x20;

### Hide/show

You can temporarily hide or show annotations from the three dot drop down menu. You can also hover over any annotation and use the `H` keyboard shortcut.

### Delete

To delete an annotation, you can select/hover over it and use the delete/backspace keyboard shortcut. Alternatively, you can delete an annotation from the three dot drop down menu.&#x20;

{% embed url="https://www.loom.com/share/ed696f060f2042be82608cf43f19c455" %}
Lock, hide, delete
{% endembed %}
