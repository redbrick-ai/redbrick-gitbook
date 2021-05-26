# Configuring AWS S3 Storage

This section covers how to prepare your Amazon S3 storage to import data into the RedBrick AI platform. After following the instructions in this section, you will be able to create an Amazon S3 'storage method' on the RedBrick platform to connect your S3 bucket to your RedBrick account.

#### Signing Up for AWS <a id="signing-up-for-aws"></a>

The first step to preparing data storage on Amazon S3, is to sign up for an AWS account on [https://aws.amazon.com.](https://aws.amazon.com/)

#### Create an S3 Bucket <a id="create-an-s3-bucket"></a>

Once you are logged in to your AWS account, head over to the Amazon S3 console. Create a new bucket, and keep all the default settings \(you can choose to change the region of the S3 bucket\). After creating your S3 bucket, upload your images through the User Interface, or use the AWS CLI for large amounts of data.

#### S3 Bucket Settings <a id="s3-bucket-settings"></a>

To ensure your data is private and secured, RedBrick uses pre-signed URL's to render data in browsers. To allow RedBrick to use pre-signed URL's to serve data, you need to define a CORS policy on the S3 bucket. [Here](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html) is the AWS S3 documentation on CORS.

To set the proper CORS policy, go to the Permissions tab in your S3 bucket. Under Permissions select the CORS configuration and copy paste the following block of code.

```javascript
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "PUT",
            "POST",
            "DELETE",
            "GET"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": [
            "x-amz-server-side-encryption",
            "x-amz-request-id",
            "x-amz-id-2"
        ],
        "MaxAgeSeconds": 3000
    }
]
```

#### Access and Secret Keys <a id="access-and-secret-keys"></a>

If your S3 Bucket blocks public access to the data, you will have to create an IAM user to allow RedBrick to securely access the data in your S3 bucket. AWS IAM enables you to manage access to your AWS services. You can read about IAM in the [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html).

To create an IAM user from the AWS console, follow these steps:

* Sign in to the AWS Management Console and open the IAM console
* In the IAM console navigation pane, choose Users and then choose Add user.

Add User

* Type the user name for the new user.
* Select Programmatic Access

Permissions

* Click on Attach existing policies directly
* Create a new policy
* Paste the following block of JSON inside the JSON tab. Remember to replace `<your_s3_bucket_name_here>` with the name of the S3 bucket that has your data. You can modify the Resource path for added security or specificity.

```javascript
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RedBrickLabelingReadOnly",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::<your_s3_bucket_name_here>/*"
    }
  ]
}
```

* Review your policy and create it.
* Head back to your IAM user creation and attach the policy you just created.

{% hint style="info" %}
**Granular Permissions**  
  
You can configure your S3 bucket to give RedBrick AI access to particular data points inside your s3 bucket by modifying the "Resource" section in the file above. 
{% endhint %}

Create the user

* Create the user and download Access and Secret key .csv
* Store the CSV file with your keys carefully.

