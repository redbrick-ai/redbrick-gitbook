# Configuring AltaDB

This section covers how to prepare your AltaDB storage to import data into the RedBrick AI platform. After following the instructions in this section, you will be able to create an AltaDB 'storage method' and import Data into RedBrick AI.&#x20;

### Signing up on AltaDB Platform <a href="#signing-up-for-google-cloud-platform" id="signing-up-for-google-cloud-platform"></a>

The first step is to [create an account](https://docs.altadb.com/altadb) on AltaDB.

### Dataset Creation & Importing Data&#x20;

1. Create a dataset.
2. Click on Import data, and drag & drop your DICOM files into the data importer. **AltaDB v0.0 only supports direct upload through the browser**.
3. Once the upload is complete, AltaDB will index the DICOM headers and re-compress the DICOM pixel data with state-of-the-art compression. This process will take a few minutes for 10 series.
4. You can [monitor the status of your imports](https://share.redbrickai.com/PTBs1H5P) inside the "Import" tab.

{% hint style="info" %}
Processing an import will take several minutes to completely index all DICOM headers and re-compress pixel data with state-of-the-art compression
{% endhint %}

### Viewing the Data

You can preview your images by clicking on the thumbnail. The simple viewer offers a view of the imaging axis and supports a few key functions:

1. Change slice: Mouse scroll.
2. Windowing: Right-click drag.
3. Zoom: Left-click drag.
4. Pan: Middle mouse drag.

{% embed url="https://share.redbrickai.com/y5k3NJ28" %}

## Integrating with RedBrick AI

### Create API key on AltaDB <a href="#create-api-key-on-altadb" id="create-api-key-on-altadb"></a>

To Create a new API key, Go to API keys in the left menu sidebar and click on "New API key" button on the top right corner. Once created, note down the "access" and "secret" keys.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Download the JSON from AltaDB <a href="#download-the-redbrick-ai-json-from-altadb" id="download-the-redbrick-ai-json-from-altadb"></a>

In your AltaDB dataset, select the series you want to import into RedBrick AI and click on the "Download RedBrick AI JSON button".

{% embed url="https://share.redbrickai.com/dmQRrWDT" %}

### Create AltaDB storage method on RedBrick AI

Next step is to create an AltaDB storage method in your RedBrick AI account. You will need your AltaDB Access and Secret keys to setup this storage method.

<figure><img src="../../.gitbook/assets/Screenshot 2024-06-05 at 5.29.37 PM.png" alt=""><figcaption></figcaption></figure>

### Importing Data into RedBrick AI

To import data into RedBrick AI, Upload the JSON file you downloaded from AltaDB and Select AltaDB from the dropdown in the external storage method.

<figure><img src="../../.gitbook/assets/image.webp" alt=""><figcaption></figcaption></figure>
