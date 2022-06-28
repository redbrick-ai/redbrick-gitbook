# Items List for Cloud Data

To upload data from cloud storage like AWS s3, you need to create an [items list](../../../importing-data/import-cloud-data.md#items-list) that provides file paths to your data. You can upload this items list using the CLI.&#x20;

First, you need to either [clone an existing project](../#clone-an-existing-project), or [create a new project](../#create-a-project) with the CLI. Once you do this, make sure you enter your project's directory

```
cd project-directory
```

Next, you can upload your items JSON file as follows:&#x20;

```
redbrick upload ./path/to/items.json --json --storage <storage_id>
```

`<storage_id>` is the unique ID of your RedBrick AI storage method. This ID can be found on the Storage Method page.

The upload command with the `--json` flag will recursively check the directory you have provided for a JSON file, and will assume that is the items file you'd like to upload. The following command will recursively search `./path/to/folder` for an `.json` file to upload.

```
redbrick upload ./path/to/folder --json --storage <storage_id>
```
