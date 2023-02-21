# Import Cloud Data

The data that you use with RedBrick AI can be stored in a number of places. You can upload data directly to the RedBrick AI platform or integrate an external storage method such as Amazon S3, Google Cloud Platform, or Azure Blob Storage. Using your own external storage method allows you to manage the storage of your raw data, including granular level access and privacy control.

While the steps and configurations required for uploading data from cloud storage vary depending on your provider, the overall procedure remains the same:&#x20;

1. Configure Cloud Storage
2. [Create & Configure Storage Method](./#creating-and-configuring-a-storage-method)
3. [Create & Upload an Items List](./#creating-and-configuring-your-items-list)
4. Import Data

### Configuring Cloud Storage

RedBrick AI currently supports the following external storage methods:

* [AWS S3 Buckets](configuring-aws-s3.md)
* [Google Cloud Storage](configuring-gcs.md)
* [Azure Blob Storage](configuring-azure-blob.md)
* Public - this includes data stored on your computer, as well as data stored on any public server accessible via URL

{% hint style="info" %}
All data uploaded via [Direct Upload](../direct-data-upload.md) will be stored securely on RedBrick AI’s servers.
{% endhint %}

If you find yourself in need of further clarification, we recommend consulting our in-depth configuration guides for the above third-party cloud storage solutions.

Once you have configured your cloud storage, you can return to the RedBrick AI platform to proceed with creating and configuring your Storage Method.



### Creating & Configuring a Storage Method

After opening the Storage tab in the lefthand sidebar, click on **New Storage Method** to configure your new Storage Method for further use with RedBrick AI. After inputting the required credentials, click on **Create Storage** to integrate your cloud storage with RedBrick AI.

You can also make use of the **Verify** action to ensure that your file path has been correctly designated and integrated with RedBrick AI.



### Creating & Configuring an Items List

Your Items List is a JSON file that points the RedBrick AI platform to the data in your external storage and allows you to selectively import data points. It can be uploaded to RedBrick from the Project Dashboard or by using the [SDK](../../python-sdk/sdk-overview/importing-data-and-annotations.md).

<figure><img src="../../.gitbook/assets/items_list_popout.png" alt=""><figcaption><p>Clicking on Import Data will allow you to upload your Items List</p></figcaption></figure>

The format of your Items List depends on both the type of cloud storage you have integrated with RedBrick AI and the type of data you are uploading.

For solution-specific instructions regarding how to format your Items List with [AWS S3](configuring-aws-s3.md#items-path), [GCS](configuring-gcs.md#items-path), or [Azure Blob Storage](configuring-azure-blob.md#items-path), please refer to the corresponding configuration guide.

{% hint style="info" %}
Please note that there is no need to create an Items List when using [Direct Upload](../direct-data-upload.md).
{% endhint %}

For a more detailed overview of how Items Lists work in RedBrick AI, as well as examples of how to format them with different data types, please consult our dedicated [guide](creating-an-items-list.md).



### Data Privacy

When using an external storage method with RedBrick AI, all of your data is transferred directly from your storage method to your browser.

<figure><img src="../../.gitbook/assets/Group 476.png" alt=""><figcaption></figcaption></figure>

Your raw data will never be routed through RedBrick AI's servers, downloaded, or duplicated (unless specifically requested for certain features - please review our [Privacy Policy](https://redbrickai.com/policies/privacy.pdf)).&#x20;
