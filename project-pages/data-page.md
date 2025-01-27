# Data Page

The Project Data Page is where you can find your Project's Tasks, [Task Histories](../projects/tasks-and-assignment.md), Task States, and a variety of other metrics about the work done by your team.

All Org Admins, Project Admins, and Project Managers can view all of the Tasks on the Data Page and make use of its filtering and reporting capabilities to effectively manage, track, and assign Tasks.

The Data Page consists of several subsections, as seen below:

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 13.19.29@2x.png" alt=""><figcaption><p>Sections of the Data Page</p></figcaption></figure>

1. Lefthand toolbar
2. Filters
3. Search bar
4. Quick Settings
5. Task List
6. Individual Task
7. Footer (and Snackbar)

***

## Lefthand Toolbar

The lefthand toolbar has two modes, depending on how you are viewing your RedBrick AI Tasks.

### Analytics Mode

If you are viewing Tasks in **Analytics Mode** (i.e. you have not activated Folder Mode), the lefthand toolbar will display productivity information for the selected user based on the date range provided. Analytics Mode is the standard view for all Projects.

Users with relevant permissions can click on the chevron next to their name to expand a list of team members that have been added to the Project Workforce.

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 13.29.30@2x.png" alt=""><figcaption><p>The Workforce dropdown</p></figcaption></figure>

Selecting any user will then allow you to apply the time time-based filters to them, and reveal the corresponding labeler or reviewer productivity information.

### Folder Mode

**Folder Mode** allows you to apply verticality to your Task navigation in RedBrick AI, and easily move between subsets of your Tasks as needed based on the Task names provided on upload.

When you are in **Folder Mode**, the lefthand toolbar will populate with all of the directories and subdirectories that were supplied in the Task upload.

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 13.43.01@2x.png" alt=""><figcaption><p>Viewing your Project in Folder Mode</p></figcaption></figure>

In the example above, we see that:

* the parent folder `ParentJ` contains 1 sub-folder and 1 bottom-level folder: `ChildC` and `ChildJ`, which are visible in the center of the page
* Sub-folder `ChildC` contains a bottom-level folder called `GrandchildE`
* Bottom-level folder `GrandchildE` contains 1 RedBrick Task
* Bottom-level folder `ChildJ` contains 3 RedBrick Tasks

Clicking into `ChildJ` (which can be done either in the lefthand toolbar or in the center of the page) reveals 3 Tasks:

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 13.48.17@2x.png" alt=""><figcaption><p>Viewing a bottom-level folder in Folder Mode</p></figcaption></figure>

In the screenshot above, the full Task name (`ParentJ/ChildJ/BraTS2021_00004`) is visible, which also demonstrates how RedBrick creates folders based on the **location of front slashes in the Task name**.

***

## Filters

RedBrick AI allows you to sort Tasks by a variety of filters based on Task state, assignment, Stage, and more.

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 15.28.34@2x.png" alt="" width="563"><figcaption></figcaption></figure>

Please note that Task filters can be further sorted by user in order to return even more specific queries, e.g.:

* `Issues -> Label Stage -> Bob Ross` to return all Issues submitted by annotator Bob Ross
* `Recently reviewed -> Review_2 -> Dmytro K.` to display all Tasks in the Review\_2 Stage recently examined by Dmytro K.

***

## Search Bar

The **Search Bar** can be used to search for partial or full Task Names or Task IDs.

If your team employs a standardized naming convention and stratified naming (e.g. "John\_Doe/studyA/timepoint1/scan1"), a simple search is often the easiest way to display a subset of Tasks.

***

## Quick Settings

The **Quick Settings** icons display at the top right of each Project to give you a sense of which configurations are active in your Project.&#x20;

Click on any of the icons to be redirected to the corresponding Project Settings tab.

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 15.37.26@2x.png" alt=""><figcaption><p>A snapshot of Quick Settings</p></figcaption></figure>

In the example above, we can see that the Project in question has:

* an active Label Validation Script;
* active Hanging Protocols;
* inactive Webhooks;
* caching enabled;
* no labeling instructions provided;
* Automatic Task Assignment enabled;

***

## Task List

The **Task List** is where admins can find all of a Project's Tasks and non-admins can find Tasks that have been assigned to them. All filtering and search operations, as well as folder navigation in **Folder Mode**, will return results in the center of the page.

Each row in the **Task List** represents a single [Task](../projects/tasks-and-assignment.md#what-is-a-task), and there are a variety of operations and actions available to RedBrick users here.

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 15.53.39@2x.png" alt=""><figcaption><p>A single Task</p></figcaption></figure>

* **Datapoint** - otherwise known as the Task Name. If this name is not defined by the user, RedBrick will use the name of the uploaded file;
* **Stage** - the Task's current location in the Project pipeline. Clicking on this icon will display the [Task History](data-page.md#task-history) for a specific Task;
* **Files** - the number of unique file paths associated with the Task;
* **Task ID** - the RedBrick-generated unique identifier for the Task, required in many SDK operations;
* **Assignee** - the Workforce member currently assigned to the Task;
* **Score** - in cases of [Consensus](multiple-labeling/consensus/) or [Labeler Evaluation](../projects/labeler-evaluation.md) Projects, a [RedBrick-calculated agreement score](multiple-labeling/consensus/agreement-calculation.md) based on the labeler's work;
* [**Task Analytics**](../projects/project-and-task-analytics.md#task-analytics) (on mouse hover) - an icon that can be clicked to display a variety of metrics related to the annotation work done on the Task;
* **Caching Icon** - an icon that shows the Task has been cached in your local browser (and is therefore present in your [Worklist](../dashboard/worklist.md)). Clicking on this button will un-cache the contents of the Task from your browser;
* **Three-dot Menu** - an expandable dropdown menu that contains many Task-related actions;
* **Go to Task button** - click to open the Task in your current tab;

***

### Task History

You can access a comprehensive list of Task events by clicking on the Task's Stage, bringing the functionality of the Python SDK's [`get_task_events()` function](https://sdk.redbrickai.com/sdk.html#redbrick.export.Export.get_task_events) to the Dashboard.

<figure><img src="../.gitbook/assets/CleanShot 2024-09-12 at 13.30.52@2x.png" alt=""><figcaption><p>A sample Task History for a Task in the Review_1 Stage</p></figcaption></figure>

***

### Three-dot Menu

The three-dot menu on the righthand side of the Task row includes a variety of Task actions.&#x20;

* Open in Editor
* Send to Stage
* Cache Task
* View Task Analytics
* Export Comments
* Delete Task
* Archive Task

The three-dot menu can also contain Stage-specific actions, such as **Set as** [**Reference Standard**](../projects/reference-standards.md).&#x20;

***

### Send to Stage

The **Send to Stage** action allows the user to move a Task from one Project Stage to another, overriding the standard project workflow.&#x20;

Sending a Task to a different Stage may be useful if:

* As a labeler, you want to make edits to a Task you have already finalized;
* As an admin, you need to return a Task to a previous Stage without sending it all the way to the beginning of your pipeline;
* As an admin, you need a Task to skip over the review pipeline you've established;

To send a Task to a different Stage, simply access the Task's three-dot menu on the Data page and click on the desired destination Stage.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption><p>The Send to Stage action</p></figcaption></figure>

***

## Footer

The **Footer** of the Data Page contains information about:

* the number of Tasks you are currently displaying per Page;
* the Page you are currently viewing;
* the total number of Pages;
* the total number of Tasks in your Project;

When you select a Task(s), a snackbar will appear at the bottom of the screen that will allow you to easily mass export Comments, assign, and delete Tasks.

<figure><img src="../.gitbook/assets/CleanShot 2024-12-11 at 16.54.14@2x.png" alt=""><figcaption><p>The assignment snackbar</p></figcaption></figure>
