# Configure external annotation storage

For `DICOM_SEGMENTATION` projects, you can configure your project to store annotations in an external storage location like AWS s3, Azure, or GCP. First, you need to create a RedBrick AI Storage Method integration with your cloud provider - make sure to enable read and write permissions on the bucket.&#x20;

Once you have your bucket set up with the correct permissions, run the following commands to change your _project wide_ annotation storage to your bucket.&#x20;

```python
import redbrick

org_id = "TODO"
project_id = "TODO"
api_key = "TODO"

# Get the project object
project = redbrick.get_project(org_id, project_id, api_key)

storage_id = "TODO" # This is your storage method with read/write permissions
project.set_label_storage(storage_id, "todo/path/to/storage/location")
```

Once you do this, all NIfTI annotations will be stored within the path you specified inside your storage method.&#x20;

{% hint style="info" %}
You only need to run this once per project
{% endhint %}
