# Organization and Project Roles

## Overview

Your **Organization** is a unique structure that RedBrick AI creates for you and your team.

All of the work you do on RedBrick AI and any resources you use will be housed within your Organization. This includes your team members, your Taxonomies, your Projects, and more.

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

In RedBrick AI, a **Project** is a workspace to which you can upload data and inside of which you perform annotation work within a pipeline defined by you.&#x20;

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

Within a Project, you can:

* upload images, volumes, and segmentation files;
* [assign work to your labelers and reviewers](https://docs.redbrickai.com/projects/task-assignment) on a Task level;
* perform and review annotation work;
* define [Project-level permissions](what-is-an-organization.md#project-level-roles) for labelers, reviewers, administrators, etc.;
* [invite specific members of your team](what-is-an-organization.md#inviting-members) and regulate their access to various Stages;
* view a range of statistics on the quality of your labelers' work, time spent;
* configure [custom toolkits](https://docs.redbrickai.com/annotation/layout-and-multiple-volumes/custom-hanging-protocol) and [Project-level settings](https://docs.redbrickai.com/projects/consensus-inter-annotator-agreement) specific to your use case;
* and much, much more!

While all of your team members have to be invited to your Organization in order for them to access RedBrick AI, you can easily [configure their permissions](what-is-an-organization.md#common-role-configurations) based on their Roles.

## Roles

RedBrick AI offers role-based access control at two levels - the **Organization level** and the **Project level**. Each of these roles governs what actions a user can perform at the respective level.

<figure><img src="../.gitbook/assets/Label evaluation@2x (1) (2).png" alt=""><figcaption></figcaption></figure>

### Organization-level Roles

While each Organization can only have a single **Org Owner**, there is no limit to the number of **Org Admins** and **Org Members** an Organization can have.

<table data-header-hidden><thead><tr><th width="297">Role</th><th>Permissions</th></tr></thead><tbody><tr><td>Org Owner</td><td><strong>Organization Level:</strong> Has access to all assets within an Organization; has the ability to create, edit, and delete assets, including the Organization itself. <br><br><strong>Project Level:</strong> Org Owners are automatically added to all Projects as Project Admins (see below).</td></tr><tr><td>Org Admin</td><td><strong>Organization Level:</strong> Has access to all assets within an Organization; has the ability to create, edit, and delete assets, but not the Organization itself. <br><br><strong>Project Level:</strong> Org Admins are automatically added to all Projects as Project Admins (see below).</td></tr><tr><td>Org Member</td><td><strong>Organization Level:</strong> cannot create or edit resources at the Organization level. <br><br><strong>Project Level:</strong> Org Members are <strong>not</strong> automatically added to any Projects, and <strong>must be invited</strong> to a Project by a Project Admin (see below).</td></tr></tbody></table>

### Project-level Roles

<table><thead><tr><th width="299">Role</th><th>Permissions</th></tr></thead><tbody><tr><td>Project Admin</td><td>Can perform administrative actions at the Project level, i.e. uploading data, assigning Tasks, editing Project Settings, and viewing Project Overview statistics &#x26; other user statistics.</td></tr><tr><td>Project Member</td><td>Can only annotate/review data (i.e. Tasks) that are assigned to them. Cannot view the activity of any other users. </td></tr><tr><td>Project Manager</td><td>Can manage Tasks and user permissions. Cannot access Project settings. </td></tr></tbody></table>

### Common Role Configurations

* **Labelers** are often first added to an Organization as Org Members, added to relevant Projects as Project Members, and given access to the Label Stage by a Project Admin.
* **Internal Reviewers** are often first added to an Organization as Org Members and then added to relevant Projects as Project Admins, which gives them Project-wide Admin access.
* **External Reviewers** are often first added to an Organization as Org Members, added to relevant Projects as Project Members, and given access to any relevant Review Stages by a Project Admin.
* **External Project Managers** should be added to an Organization as Org Members and added to relevant Projects as Project Managers.

## Configuring Team Member Permissions

REMEMBER - permissions on RedBrick are split into Organization-level and Project-level.

### Configuring Organization-level Permissions

Organization-level permissions are configured on the Teams Page by the Org Owner. Simply open the Teams Page and edit the entry in the Role column as needed.

<figure><img src="../.gitbook/assets/CleanShot 2025-01-08 at 13.57.43@2x.png" alt=""><figcaption><p>Changing a Team member's Organization-level permissions</p></figcaption></figure>

### Configuring Project-level Permissions

Project-level permissions are configured within a Project's Workforce tab.

Assigning a Project Member to a particular Stage restricts their access to **only those Tasks that are currently in that specific Stage**. This restriction applies to both manual and automatic task assignment.&#x20;

If you are an Org Admin, you can add Org Members with more limited permissions to a Project by:

* Navigating to the Project's Workforce tab;
* Clicking **Add Org Member** (Step 1 below);
* Selecting the Org Member you'd like to add (Step 2);
* Selecting the required permissions level (Step 3);
* Clicking **Add to Project** (Step 4);

<figure><img src="../.gitbook/assets/CleanShot 2025-01-08 at 13.54.08@2x.png" alt=""><figcaption><p>Adding Org Members to a Project</p></figcaption></figure>

## Designating and Changing an Organization Owner

By default, the Org Owner for all new RedBrick Organizations is support@redbrickai.com.

If you would like to change your Org Owner, please reach out to our support team at support@redbrickai.com.&#x20;

