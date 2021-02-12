# Importing Data into a Dataset

The data that you use with the RedBrick AI platform can be stored in a number of places, including locally on your computer, on Amazon S3, or another cloud provider. The RedBrick AI data warehouse integrates with your existing storage method to give you full control over the data privacy and access. 

To import data into your dataset, you need to: 

* [Create a dataset.](creating.md#creating-a-dataset)
* Select the [storage method](storage-methods.md) to which you want to integrate to.
* Upload an [items list](preparing-your-data.md#prepare-your-items-list) specifying which data-points from your storage method you want to import.

## Prepare Your Items List

The items list points the RedBrick AI platform to the data points in the data storage. This way you can selectively import data points from a storage method. The items list is a JSON file which comprises of a list of entries of the following format.

```javascript
{
    "url": "<filepath_of_datapoint>",
    "name": "<name_of_datapoint>" // Needed for videos
}
```

Here is a sample item list entry for each of the possible storage methods.

{% tabs %}
{% tab title="AWS S3" %}
Say your datapoint `image.png` is stored inside a folder named `folder` inside an s3 bucket, the item list entry for that datapoint will be.

```javascript
{ 
  "url": "folder/image.png" 
}
```
{% endtab %}

{% tab title="Local Storage" %}
Say your data point `image.png` is stored inside a folder named `folder` which is being hosted using an http server on `http://127.0.0.1:8000/`, the item list entry for that datapoint will be.

```javascript
{
  "url": "http://127.0.0.1:8000/folder/image.png"
}
```
{% endtab %}

{% tab title="Public Cloud Storage" %}
Say your datapoint is hosted at a public endpoint `https://path/to/data/image.png`, the item list entry for that datapoint will be.

```javascript
{
  "url": "https://path/to/data/image.png"
}
```
{% endtab %}
{% endtabs %}

### Image Items List

The items list for importing images into the RedBrick AI platform is simply a list of item list entries. Each entry will be a single datapoint on the RedBrick AI platform. The item list below will import three datapoints into the RedBrick AI platform.

```javascript
  [
    {
      "url": "folder1/image1.png"
    },
    {
      "url": "folder1/image2.png"
    },
    {
      "url": "folder2/image1.png"
    }
  ]
```

### Video Items List

The items list for importing images into the RedBrick AI platform is slightly different than images. Videos have to be parsed into frames and be imported into the RedBrick AI platform. Say you have two videos - `video1`, `video2`, that you want to import into the platform, and each video has three frames - `frame1.png`, `frame2.png`, `frame3.png`. The items list for this would be.

```javascript
  [
    {
      "url": "video1_folder/frame1.png",
      "name": "video1"
    },
    {
      "url": "video1_folder/frame2.png",
      "name": "video1"
    },
    {
      "url": "video1_folder/frame3.png",
      "name": "video1"
    },
    {
      "url": "video2_folder/frame1.png",
      "name": "video2"
    }
    {
      "url": "video2_folder/frame2.png",
      "name": "video2"
    }
    {
      "url": "video2_folder/frame3.png",
      "name": "video2"
    }
  ]
```

Using this items list, two video datapoints \(video1, video2\) will be imported into the platform with three frames each. The frames of each video will be ordered in the same order as their appearance in the items list.

### Programmatically Generate Items List For S3

If you don't have a standard naming convention for your files inside your s3 bucket, or you're not sure which files are in the s3 bucket, you can use the AWS CLI to enumerate a list of all the objects inside a bucket. Using this list, you can programmatically generate an items list.

#### Installing and Configuring the AWS CLI <a id="installing-and-configuring-the-aws-cli"></a>

Have a look at the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) for installing the CLI. For mac users, running `brew install awscli` is the easiest way to install the AWS CLI.

Once you have the AWS CLI installed, you need to configure the cli with your AWS root account Access Key and Secret Key to give permissions to AWS CLI. After installing AWS CLI, do the following.

```bash
$ aws configure
AWS Access Key ID [None]: <your_access_key>
AWS Secret Access Key [None]: <your_secret_key>
Default region name [None]:
Default output format [None]:
```

After filling out your keys, you can leave the last two fields empty.

Now that your AWS CLI is configured, you can list out the objects inside your s3 bucket by running the following command.

```bash
$ aws s3 ls s3://<your_bucket_name>
```

After listing out all the images inside the s3 bucket \(or a folder in the bucket\), you can save the output to a txt file and write a simple script to convert that output into a JSON file in the format of the Items List covered above.

