# Configuring external storage

The data that you use with the RedBrick AI platform can be stored in a number of places, you can upload data directly to the platform or integrate an external storage method to store your data like Amazon S3, Google Cloud Platform, or Azure Blob Storage. By using your own external storage method, you can manage the storage of your raw data, including granular level access and privacy control.

You can see the external storage method data model on the RedBrick AI model. When data is stored externally, your raw data will never be routed via RedBrick AI servers, nor will it be downloaded/duplicated (unless specifically requested for certain features, please review our [Privacy Policy](https://redbrickai.com/policies/privacy.pdf)). The data is transferred directly from your storage method to your browser.&#x20;

![RedBrick AI external storage data model.](../../.gitbook/assets/group-476.png)

## Configure a Storage Method

Currently, the options for external Storage Methods are:

* [AWS S3 Buckets](broken-reference).
* [Google Cloud Storage.](broken-reference)
* [Azure Blob Storage.](broken-reference)
* [Public](broken-reference). This storage type includes data stored on your computer and data stored on any public server accessible by a URL.&#x20;
* [Direct Upload](broken-reference). This storage type allows you to store your data securely on RedBrick AI servers without having to configure your own storage method.

You can create a storage method by clicking on the **Storage Method **_****_ on the left side bar of your account. On the storage method page, click on **Create Storage Method**. _****_&#x20;

## Upload an Items List to Your Project

{% hint style="info" %}
For [Direct Upload](broken-reference) i.e. uploading your image files directly to RedBrick AI servers, you don't have to create an items list.&#x20;
{% endhint %}

The items list points the RedBrick AI platform to the data points in the data storage. This way you can selectively import data points from a storage method. Once you create your JSON items list, you can upload it through the UI, or [SDK](../../python-sdk/sdk-overview/importing-data-and-annotations.md#creating-data-points-without-labels).

![Upload your items list from the project dashboard](<../../.gitbook/assets/Screen Shot 2022-02-23 at 3.19.08 PM.png>)

![Select your Storage Method type, and upload your items file](<../../.gitbook/assets/Screen Shot 2022-02-23 at 3.20.56 PM.png>)
