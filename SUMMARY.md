# Table of contents

* [About RedBrick AI](README.md)

## Team & Organization <a href="#organizations" id="organizations"></a>

* [Invite your team to your organization](organizations/what-is-an-organization.md)
* [Roles and Permissions](organizations/teams-and-permissions.md)
* [Invite labelers to your Project](organizations/invite-labelers-to-your-project.md)

## Importing Data

* [Direct data upload](importing-data/direct-data-upload.md)
* [Import Cloud Data](importing-data/import-cloud-data.md)
* [Configuring external storage](importing-data/configuring-external-storage/README.md)
  * [Configuring AWS s3](importing-data/configuring-external-storage/configuring-aws-s3.md)
  * [Configuring GCS](importing-data/configuring-external-storage/configuring-gcs.md)
  * [Configuring Azure Blob](importing-data/configuring-external-storage/configuring-azure-blob.md)

## Projects

* [How project pipelines work](projects/how-project-pipelines-work.md)
* [How task assignment works](projects/how-task-assignment-works.md)
* [Taxonomies (V1)](projects/taxonomies-v1.md)
* [Taxonomies (V2)](projects/taxonomies-v2.md)
* [Consensus (Inter-annotator Agreement)](projects/consensus-inter-annotator-agreement/README.md)
  * [Agreement calculation](projects/consensus-inter-annotator-agreement/agreement-calculation.md)
* [Custom Label Validation](projects/custom-label-validation.md)
* [Custom hanging protocol](projects/custom-hanging-protocol.md)

## DICOM Annotation

* [Overview](dicom-annotation/overview.md)
* [Creating, editing and deleting annotations](dicom-annotation/creating-editing-and-deleting-annotations.md)
* [Filters - windowing, thresholding etc.](dicom-annotation/filters-windowing-thresholding-etc..md)
* [Layout - series/study](dicom-annotation/layout-series-study.md)
* [Multiple Modalities](dicom-annotation/multiple-modalities.md)
* [Segmentation](dicom-annotation/segmentation/README.md)
  * [Instance vs. Semantic](dicom-annotation/segmentation/instance-vs.-semantic.md)
  * [Overlapping Segmentations](dicom-annotation/segmentation/overlapping-segmentations.md)
  * [Segmentation mirroring](dicom-annotation/segmentation/segmentation-mirroring.md)
  * [Intellisync](dicom-annotation/segmentation/intellisync.md)

## Python SDK & CLI <a href="#python-sdk" id="python-sdk"></a>

* [SDK Overview](python-sdk/sdk-overview/README.md)
  * [Exporting Annotations](python-sdk/sdk-overview/exporting-annotations.md)
  * [Importing Data and Annotations](python-sdk/sdk-overview/importing-data-and-annotations.md)
  * [Label and Review](python-sdk/sdk-overview/label-and-review.md)
  * [Create a Project](python-sdk/sdk-overview/create-a-project.md)
  * [Configure external annotation storage](python-sdk/sdk-overview/configure-external-annotation-storage.md)
* [CLI Overview](python-sdk/cli-overview/README.md)
  * [Exporting Annotations](python-sdk/cli-overview/exporting-annotations.md)
  * [Importing Data](python-sdk/cli-overview/importing-data/README.md)
    * [Direct Upload to RedBrick](python-sdk/cli-overview/importing-data/direct-upload-to-redbrick.md)
    * [Items List for Cloud Data](python-sdk/cli-overview/importing-data/items-list-for-cloud-data.md)
  * [Importing Annotations](python-sdk/cli-overview/importing-annotations/README.md)
    * [NIfTI Segmentations](python-sdk/cli-overview/importing-annotations/nifti-segmentations.md)
    * [Vector Annotations](python-sdk/cli-overview/importing-annotations/vector-annotations.md)
  * [Configure external annotation storage](python-sdk/cli-overview/configure-external-annotation-storage.md)
* [Format Reference](python-sdk/reference/README.md)
  * [Annotation Format](python-sdk/reference/annotation-format.md)
  * [TaxonomyObject](python-sdk/reference/taxonomyobject.md)
  * [TaskObject](python-sdk/reference/taskobject.md)
* [Full SDK Reference](https://redbrick-sdk.readthedocs.io/en/stable/)

## Useful Links

* [Privacy Policy](https://redbrickai.com/policies/privacy.pdf)
