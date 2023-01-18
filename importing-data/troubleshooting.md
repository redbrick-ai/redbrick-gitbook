# Troubleshooting

This section covers troubleshooting issues in loading data in the annotation tool. If there is an error in loading your data, you will encounter the following error screen.&#x20;

<figure><img src="../.gitbook/assets/Screen Shot 2023-01-18 at 4.21.35 PM.png" alt=""><figcaption></figcaption></figure>

Here are recommended steps for troubleshooting your loading issues:&#x20;

1. You may have a specific error message under "Failed to load image." This **error message could provide insight** into why your task is not loading. In the image above, "Request failed with status code 404" likely means an [external storage integration](configuring-external-storage/) or internet connection issue.
2. If you're using external storage and can see URLs enumerated under "Failed to load these URLs," try opening the link in your browser.&#x20;
   1. If the browser loads a screen with an error message, there is likely an **issue with your Storage Method integration** (possibly your bucket name or access keys). You can double-check the validity of your storage method integration using the "Verify" function within the Storage Method tab. It is also possible that your Storage Method integration is valid, but the item's path __ you have provided is invalid, i.e., the data point doesn't exist in your bucket.
   2. If the browser downloads the data file (or displays it, in the case of .png, .jpeg, etc.), you probably **have not enabled CORS on your bucket**. If CORS is not enabled on your bucket, your browser will not be able to load the image (because it [originates from a different _origin_](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)_)._
3. If you have double-checked the validity of your Storage Method integration & items paths and enabled CORS on your bucket, the issue in loading the data is likely because of the image file's contents. Here are some possible problems:&#x20;
   1. Your DICOM or NIfTI files may not be wholly defined, i.e., have all required headers for us to display the image.&#x20;
   2. If you see the error message "Set maximum size exceeded," this means you have uploaded an annotation file with an instance ID greater than 256. This could happen if you accidentally import an _image file_ in the [segmentation](../python-sdk/reference/annotation-format.md#segmentations)[s](../python-sdk/reference/annotation-format.md#segmentations-string-or-string) field in the items file.&#x20;
   3. Our interface is expecting NIfTI files of type UInt8. If you import image or annotation files with floating point values, you will get the following error message "Values must be integers."
