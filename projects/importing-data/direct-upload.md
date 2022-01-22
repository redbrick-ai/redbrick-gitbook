# Direct Upload

## Adding Files for **D**irect Upload

This section will cover how to get started immediately by uploading files directly to our RedBrickAI servers for use via Direct Upload. This storage type allows you to store your data securely on RedBrick AI servers without having to configure your own storage method. This will automatically upload your data to our secure cloud and create tasks for your projects without any further setup steps.

## Image or Document Projects

This is a simple process of just uploading the files that you want to use to create tasks. Each file will be made into a task that can be used further in your project pipeline. The task will have its name set by default to the file name.

{% hint style="warning" %}
Files that are uploaded with the same file name to a single project will fail. Each file must have a unique name.&#x20;
{% endhint %}

![Direct Upload for Images and Documents](../../.gitbook/assets/Direct-Upload-Image-Cropped.PNG)

Each file uploaded will be made into its own task. As shown in the image below, `pricinglvl2.png` and `pricinglvl3.png` will be made into separate tasks respectively. Simply click _Start Import_ and you are ready to go!

![Image Upload Read](../../.gitbook/assets/DirectUpload-Image-Done-Cropped.PNG)





## Video Projects <a href="#video-projects-beta" id="video-projects-beta"></a>

For video projects you can upload MP4 files and we will handle the parsing down to frames. Videos will be split into frames at the full frame rate of the videos. Any frames beyond the first 5000 will be removed. It is strongly recommended to keep video clips shorter to assist annotators.&#x20;

## DICOM Projects <a href="#video-projects-beta" id="video-projects-beta"></a>

For DICOM projects you can upload _.dcm_ series folders and we will create separate tasks for each folder uploaded. For folders that contains multiple sub-folders, each sub-folder will be counted as a separate folder and create a separate task. It is strongly recommended to not upload too many tasks at once as web browsers might not be able to handle the amount of data or threshold data transfer limits, leading to subpar performance.&#x20;

{% hint style="warning" %}
Only multiple _.dcm_ file series are currently accepted. Single ._dcm_ files are not currently supported.
{% endhint %}

![DICOM Direct Upload](../../.gitbook/assets/dicom-upload.png)

As shown in the image above,  `SE000001` is the folder containing the series of DICOM files to be uploaded and will be made into a single task. Simply click _Start Import_ and you are ready to go!

![Data inside SE000001](../../.gitbook/assets/test-data-dicom.png)
