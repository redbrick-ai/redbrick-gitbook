# Configure external annotation storage

You can configure your project to store annotations in an external storage location like AWS s3, Azure, or GCP. First, you need to create a RedBrick AI Storage Method integration with your cloud provider - make sure to enable **read and write permissions** on the bucket.&#x20;

First, set up your CLI, and [clone or create a new project](./).

```bash
// Inside your project-directory
redbrick info set labelstorage
> Storage ID: <storage_id>
> Path prefix: path/to/label/directory
```

`<storage_id>` is a unique ID for your cloud storage method that can be found within the Storage Methods tab.&#x20;

`Path prefix` is the directory in your cloud bucket, within which your annotation files are. **Note - the file paths in the `segmentation` entry of your items list will be relative to this path.** You can leave it as the root of your bucket by defining it as `.`.

{% hint style="warning" %}
Once you set your projects annotation storage method, changing/deleting files in your cloud console can cause issues with your RedBrick AI projects. RedBrick AI will expect to find the annotation files in your bucket.
{% endhint %}
