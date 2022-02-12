# Taxonomies

Taxonomies provides a structured way of defining your object label categories. Taxonomies allow you to re-use a set of label classes and attributes over different projects. A simple taxonomy is shown below

![](<../.gitbook/assets/image 440 (1).png>)

### **Creating A Taxonomy**

You can create a non-nested taxonomy using simple creation, or build a taxonomy from scratch using the JSON editor. Each taxonomy includes a category and an attribute section. The category has:

* A unique category name
* A unique category ID \[0,n) where n is the number of classes.
* A color that will be used when displaying the label

While in the create a taxonomy modal, type a category name and press enter to add it to the taxonomy list. Each taxonomy entry can have child categories as well, up to a depth of 3 levels.

![](<../.gitbook/assets/image 501.png>)

The attributes list comprises of

* An attribute name
* A drop down to choose between whether the attribute be a text field or a boolean&#x20;
* A toggle button to choose which categories the attribute is assigned to

An attribute can be created by clicking on 'add an attribute' button. By default, a created attribute will be assigned to all categories unless the toggle is disabled. When disabled, a link to assign categories will appear. You can select the categories that you want the attribute to applied to by selecting them from the category list.

![](<../.gitbook/assets/Group 28362.png>)

The users can also create task specific categories under the 'task classify' tab which can be used mainly to classify a task based on types. The flow and functionality of the process is identical to the categories section.
