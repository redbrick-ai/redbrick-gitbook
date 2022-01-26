# Configuring Azure Blob Storage

{% embed url="https://youtu.be/8XcRjr4TtLI" %}
Video Tutorial
{% endembed %}

## Create a Storage Account

{% hint style="info" %}
If you already have a storage account, _skip_ this section, and head directly to the next section.
{% endhint %}

An Azure storage account contains all of your Azure Storage data objects, you can find the official documentation [here](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json\&tabs=azure-portal).&#x20;

1. [Sign in](https://portal.azure.com) to your Azure portal.
2. On the left portal menu, select **Storage Accounts** to list all of your storage accounts.&#x20;
3. On the **Storage Accounts** page, click **create**.

### Basics Tab&#x20;

You need to fill out the required fields under the basics tab, please refer the table below as a quick guide.

| Section          | Field                | Description                                                                                                                                                                                                                      |
| ---------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Project details  | Subscription         | Select the subscription for the new storage account.                                                                                                                                                                             |
| Project details  | Resource group       | Create a new resource group for this storage account, or select an existing one. For more information, see [Resource groups](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview#resource-groups). |
| Instance details | Storage account name | Choose a unique name for your storage account.                                                                                                                                                                                   |
| Instance details | Region               | Select the appropriate region for your storage account. For more information, see [Regions and Availability Zones in Azure](https://docs.microsoft.com/en-us/azure/availability-zones/az-overview).                              |
| Instance details | Performance          | Select your desired level of performance, or choose the default option.                                                                                                                                                          |
| Instance details | Redundancy           | Select your desired redundancy configuration.                                                                                                                                                                                    |

### Other Settings

To configure other advanced settings on your storage account, head to advanced tabs, otherwise you can continue with default settings.&#x20;

### Review + create

When you navigate to the Review + create tab, Azure runs validation on the storage account settings that you have chosen. If validation passes, you can **proceed to create the storage account**.

## Create a Container

{% hint style="info" %}
If you already have a container, please skip to the next section.
{% endhint %}

Containers organizes a set of blobs, your Azure storage account can have an unlimited number of containers. To create a container, head to your Azure portal:&#x20;

1. Head to the **Storage Accounts** page from the left portal menu, and select the **Storage Account** you want to create your container in.
2. On the left menu of the Storage Account, scroll to the **Data Storage** section, then select **Containers.**
3. Create a container by clicking on the **+ Container** button.&#x20;
4. Type in a **name** for the container, and set the **level of public access** to the container (we recommend **Private**)

## Get your Connection String

1. Navigate to your **Storage Account** on your Azure portal.&#x20;
2. In the left menu of the Storage Account, scroll to **Security + Networking**, and select **Access Keys.**&#x20;
3. On the Access Keys page, click on **Show keys** at the top, and **copy** **one of the connection strings**

## **Create a RedBrick Storage Method**

Head over to your RedBrick AI Account:&#x20;

1. Click on the **Storage Method** tab on the left sidebar, and **Create New Storage Method.**&#x20;
2. In the creation dialog, select **Azure Blob** as the storage type and enter your **connection string,** and **storage account name.**&#x20;

### Verify your Azure connection

Once you've added your Azure storage method on RedBrick AI, you can verify the connection by doing the following:&#x20;

1. First upload an image to your container within your azure storage account (e.g. `image.png`)
2. Head to the Storage Method page on RedBrick AI, and click on the **verify** button of the storage method you just created.&#x20;
3. Paste the unique path of your blob, which will be in the following format: `container_name/blob_path` . So if you uploaded `image.png` within the sub-folder `images` in your container `image-container` , your path would be `image-container/images/image.png`.
4. If the connection was successful, you should see the image appear once you verify.

## Items List

The items list points the RedBrick AI platform to the data points in the data storage. This way you can selectively import data points from a storage method. The items list is a JSON file which comprises of a list of entries of the following format.

```javascript
{
    "items": ["<filepath_of_datapoint>"]
    "name": "<name_of_datapoint>" // Needs to be unique
                                  // Required for videos, optional for images
}
```

{% hint style="info" %}
For **image uploads** the `items` array will have only a single entry. \
For **video uploads** the `items` array has to contain the frames of the video in order.&#x20;
{% endhint %}

Below is an example of a single item list entry.&#x20;

```javascript
{
    "items": ["container-name/root-folder/sub-folder/image.png"]
}
```

**NOTE - In this case the container name is an integral part of the file path. This is specific to Azure Blob Storage.**&#x20;
