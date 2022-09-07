# How project pipelines work

The RedBrick AI pipelines are a framework that you can use to structure and automate your data efforts. You can think of the pipelines like a manufacturing assembly line where there is a product that goes through various discrete processes, that involve various automated and manual processes, before being completed.&#x20;

Similarly, pipelines are a production line for your data, where you can stitch together multiple stages based on configurable logic to run automated and manual processes to label your data.&#x20;

{% hint style="info" %}
Each project has **a single pipeline** associated with it, that defines the process of that project.&#x20;
{% endhint %}

![Example pipeline, with a single label stage followed by two review stages.](<../.gitbook/assets/image 501 (2).png>)

You can see an example pipeline above, which involves a single labeling stage, followed by two review stages for quality assurance. The data you upload to the project, will flow through the pipeline following the logic laid out in the diagram. At each stage, a **task** is created and completed before moving to the next stage.&#x20;
