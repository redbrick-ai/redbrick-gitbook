# Direct Upload to RedBrick

You can use the command line interface to easily import large amounts of data. Before following this guide, make sure to [set up the credentials for the CLI](../#create-a-credentials-config).

{% embed url="https://www.loom.com/share/f6dbbe412bc042aaa67e5fec7449152f?sharedAppSource=personal_library" %}
Upload your DICOM series using the RedBrick CLI
{% endembed %}

First, you need to either [clone an existing project](../#clone-an-existing-project), or [create a new project](../#create-a-project) with the CLI. Once you do this, make sure you enter your project's directory

```
cd project-directory
```

{% hint style="warning" %}
Make sure the data type you are uploading matches the data type of the project you are uploading into. For example, DICOM and NIfTI files can only be uploaded within DICOM projects.&#x20;
{% endhint %}

## DICOM Upload

Create a directory inside which you have your `.dcm`/`.ima` files, for example:

```bash
data
└── patient-01
    └── study-01
        └── series-01
            ├── instance001.dcm
            ├── instance002.dcm
            ├── instance002.dcm
            └── instance004.dcm

```

{% hint style="info" %}
You don't have to have your data in Patient / Study / Series folder structures. The CLI will recursively crawl your directory and parse through all the DICOM files and upload each individual series as an individual task.
{% endhint %}

To upload your `data/` directory to your project, run the following command within your `project-directory`:

```
redbrick upload data
```

## NIFTI Upload

You can upload NIfTI files to your project by creating a `data/` directory and dumping your NifTI files inside that, for example:&#x20;

```
data/
 ├── series001.nii
 ├── series002.nii
 └── series3.nii.gz
```

{% hint style="info" %}
RedBrick AI supports both .nii, and zipped .nii.gz files.
{% endhint %}

To upload your `data/` directory to your project, run the following command within your `project-directory` &#x20;

```
redbrick upload data --as-nifti 
```

## Image Upload

You can upload image files to your project by creating a `data/` directory and dumping your image files inside that, for example:&#x20;

```
data/
 ├── image01.png
 ├── image2.jpeg
 └── image3.bmp
```

To upload your `data/` directory to your project, run the following command within your `project-directory` &#x20;

```
redbrick upload data
```

## Video Upload

There are two ways to upload your video files to RedBrick. First is uploading the raw video files, which will then be parsed by RedBrick into frames. Alternatively, you can upload the parsed frame sequences yourself.&#x20;

### Raw Video Upload

Create a `data` directory with your video files:&#x20;

```
data/
 ├── video01.mp4
 ├── video002.avi
 └── video3.mp4
```

To upload your `data/` directory to your project, run the following command within your `project-directory` &#x20;

```
redbrick upload data
```

### Video Frame Upload

To upload the frame sequences, create a `data` directory with sub-directories that contain the parsed video frames.

```
data
└── video-01
    ├── frame001.png
    ├── frame002.png
    ├── frame003.png
    └── frame004.png
```

To upload your `data/` directory to your project, run the following command within your `project-directory` &#x20;

```
redbrick upload data --as-frames
```
