# Configuring Azure Blob Storage

This section covers how to prepare your Azure Blob storage to import data into the RedBrick AI platform. After following the instructions in this section, you will be able to create an Azure Blob 'storage method' on the RedBrick platform to connect your Azure Blob Storage to your RedBrick account.

An Azure storage account contains all of your Azure Storage data objects: blobs, files, queues, tables, and disks. The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS. Data in your Azure storage account is durable and highly available, secure, and massively scalable.

**Create Blob storage**

**NOTE:** If you already have a Blob Storage account already, skip the following part.

1. On the Azure portal menu, select All services. In the list of resources, type Storage Accounts. As you begin typing, the list filters based on your input. Select Storage Accounts.
2. On the Storage Accounts window that appears, choose Add.
3. On the Basics tab, select the subscription in which to create the storage account.
4. Under the Resource group field, select your desired resource group, or create a new resource group. For more information on Azure resource groups, see Azure Resource Manager overview.
5. Next, enter a name for your storage account. The name you choose must be unique across Azure. The name also must be between 3 and 24 characters in length, and may include only numbers and lowercase letters.
6. Select a location for your storage account, or use the default location.
7. Select a performance tier. The default tier is Standard.
8. Set the Account kind field to Storage V2 \(general-purpose v2\).
9. Specify how the storage account will be replicated. The default replication option is Read-access geo-redundant storage \(RA-GRS\). For more information about available replication options, see Azure Storage redundancy.
10. Additional options are available on the Networking, Data protection, Advanced, and Tags tabs. To use Azure Data Lake Storage, choose the Advanced tab, and then set Hierarchical namespace to Enabled. For more information, see Azure Data Lake Storage Gen2 Introduction
11. Select Review + Create to review your storage account settings and create the account.
12. Select Create

**Create Container**

To create a container in the Azure portal, follow these steps:

1. Navigate to your storage account in the Azure portal.
2. In the left menu for the storage account, scroll to the **Blob Service** section, then select **Containers**.
3. Select the + Container button.
4. Type a name for your new container. The container name must be lowercase, must start with a letter or number, and can include only letters, numbers, and the dash \(-\) character. For more information about container and blob names, see [Naming and referencing containers, blobs, and metadata](https://docs.microsoft.com/en-us/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).
5. Keep the default level of access to the container. The default level is Private \(no anonymous access\).
6. Select OK to create the container.

#### Fetch the Connection String

1. Navigate to your storage account in the Azure portal.
2. In the left menu for the storage account, scroll to the **Settings**, then select **Access Keys**.
3. It will show you two keys and associated connection strings, click `Show Keys`.
4. Copy any one of the keys.

Use this `Connection String`  along with the  `Storage account name`  to create your storage in RedBrick AI.

