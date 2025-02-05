# Configuring GCS

This section covers how to prepare your GCS storage to import data into the RedBrick AI platform. After following the instructions in this section, you will be able to create an GCS  'storage method' on the RedBrick platform to connect your GCS bucket to your RedBrick account.

## Signing up for Google Cloud Platform

The first step to preparing data storage on GCP is to [create a account](https://cloud.google.com/) on GCP.

## Create a bucket within a project

Once you have  your GCP account and a project within your account, a bucket and upload your data within the bucket either through the UI or CLI. You can leave all the settings during creation as the default. After creating your bucket, upload your data into the bucket.&#x20;

## Create a Service Account

A service account is a special kind of account used by an application or a virtual machine (VM) instance, not a person. Applications use service accounts to make authorized API calls, authorized as either the service account itself, or as Google Workspace or Cloud Identity users through domain-wide delegation.

1. In the Cloud Console, go to the [Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) page.
2. Select the appropriate project.
3. Click Create service account.
4.  Enter a service account name to display in the Cloud Console.

    For eg, `gcs-blob-reader`

    The Cloud Console generates a service account ID based on this name. Edit the ID if necessary. You cannot change the ID later.
5. _Optional:_ Enter a description of the service account.
6. Click Create and continue to the next step.
7. Add the following two IAM roles to grant to the service account on the project.
   1. **Storage Object Viewer** (For reading the blobs from the GCS bucket)
   2. **Service Account Token Creator** (For pre-signing the blobs)
   3. If your bucket will be used as an annotation storage bucket, you need to give RedBrick AI access to PUT files as well.&#x20;
8. Once done adding roles, click Continue.
9. Click Done to finish creating the service account.
10. Note down the email id of the newly created service account.

![](<../../.gitbook/assets/Screen Shot 2021-05-26 at 10.31 1 (1).png>)

## Steps to give Bucket access to Service Account

1. In the Cloud Console, go to the [Bucket Browser](https://console.cloud.google.com/storage/browser) page.
2. Click on the more actions button (three dots) at the right of the necessary bucket.
3. Click on `Edit Bucket Permission`.
4. Click on `ADD PRINCIPAL`.
5. Add the email address of the service account created in the above step (step 10).
6.  Add following two roles

    **Storage Legacy Bucket Reader**

    **Storage Legacy Object Reader**
7. Click on save.\


## Steps to create Service Account Key (JSON)

To use a service account from outside of Google Cloud, such as on other platforms or on-premises, you must first establish the identity of the service account. Public/private key pairs provide a secure way of accomplishing this goal. When you create a service account key, the public portion is stored on Google Cloud, while the private portion is available only to you.

1. In the Cloud Console, go to the [Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) page.
2. Click the email address of the service account that we created in the above step.
3. Click the Keys tab.
4. Click the Add key drop-down menu, then select Create new key.
5. Select JSON as the Key type and click Create.
6. Clicking Create downloads a service account key file. After you download the key file, you cannot download it again.

The downloaded key has the following format, where private-key is the private portion of the public/private key pair:

```
{
  "type": "service_account",
  "project_id": "project-id",
  "private_key_id": "key-id",
  "private_key": "-----BEGIN PRIVATE KEY-----\nprivate-key\n-----END PRIVATE KEY-----\n",
  "client_email": "service-account-email",
  "client_id": "client-id",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://accounts.google.com/o/oauth2/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/service-account-email"
}
```

Make sure to store the key file securely, because it can be used to authenticate as your service account. You can move and rename this file however you would like.

#### Enable the Identity and Access Management (IAM) API

1. In the Cloud Console, go to the [API Library](https://console.cloud.google.com/project/\_/apis/library?\_ga=2.193485741.1059200516.1617769981-1501397432.1596651361) page.
2. Select the appropriate project.
3. Search for **Identity and Access Management (IAM) API** and click on it.
4. Click on `Enable`

{% hint style="info" %}
**Use this downloaded service account JSON key to create `GCS` store in the Redbrick app.**
{% endhint %}

## Configuring CORS

The final step in preparing your GCS bucket for use with RedBrick AI is enabling CORS on the bucket. Cross-Origin Resource Sharing allows the RedBrick AI application (with the domain https://app.redbrickai.com/) to make requests to your bucket.

Please visit the following Google Cloud documentation for enabling CORS on a bucket - [https://cloud.google.com/storage/docs/configuring-cors](https://cloud.google.com/storage/docs/configuring-cors).&#x20;

You will want to use the following CORS JSON configuration file:&#x20;

```javascript
[
    {
      "origin": ["https://app.redbrickai.com"],
      "method": ["GET"],
      "responseHeader": ["Content-Type"],
      "maxAgeSeconds": 3600
    }
]
```

{% hint style="success" %}
If you're also storing your annotations in your GCS bucket, be sure to add "PUT" to your method configuration array (e.g. "`["GET", "PUT"]`").
{% endhint %}

## Items Path

Once you've created your Google Storage method on RedBrick AI, you have to upload an Items List to your projects to import specific datapoints. Please have a look at the [Items List documentation](../import-cloud-data/creating-an-items-list.md#example-items-lists) for an overview of the format for the JSON file.&#x20;

For data stored in an GCS bucket, the `items` path needs to be formatted as follows:&#x20;

```json
"root-folder/sub-folder/datapoint.dcm"
```

Where `root-folder` is inside the GCS bucket storage method.
