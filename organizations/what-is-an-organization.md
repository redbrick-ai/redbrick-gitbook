# Organization and Project Roles

Everything you do on RedBrick AI will be contained within your **Organization**, including all of your  team members, projects, annotations, etc.&#x20;

### Roles

RedBrick AI offers role-based access control at two levels - the **Organization level** and the **Project level**. Each of these roles governs what actions a user can perform at the respective level.

<figure><img src="../.gitbook/assets/Label evaluation@2x (1) (2).png" alt=""><figcaption></figcaption></figure>

#### Organization-level Roles

Each Organization has a single **Org Owner**, and there is no limit to the number of **Org Admins** and **Org Members** available.

<table data-header-hidden><thead><tr><th width="297">Role</th><th>Permissions</th></tr></thead><tbody><tr><td>Org Owner</td><td><strong>Organization Level:</strong> Has access to all assets within an Organization; has the ability to create, edit, and delete assets, including the Organization itself. <br><br><strong>Project Level:</strong> Org Owners are automatically added to all Projects as Project Admins (see below).</td></tr><tr><td>Org Admin</td><td><strong>Organization Level:</strong> Has access to all assets within an Organization; has the ability to create, edit, and delete assets, but not the Organization itself. <br><br><strong>Project Level:</strong> Org Admins are automatically added to all Projects as Project Admins (see below).</td></tr><tr><td>Org Member</td><td><strong>Organization Level:</strong> cannot create or edit resources at the organizational level. <br><br><strong>Project Level:</strong> Org Members are <strong>not</strong> automatically added to any Projects, and <strong>must be invited</strong> to a Project by a Project Admin (see below).</td></tr></tbody></table>

#### Project-level Roles

<table><thead><tr><th width="299">Role</th><th>Permissions</th></tr></thead><tbody><tr><td>Project Admin</td><td>Can perform administrative actions at the Project level, i.e. uploading data, assigning Tasks, editing Project Settings, and viewing Project Overview statistics &#x26; other user statistics.</td></tr><tr><td>Project Member</td><td>Can only annotate/review data (i.e. Tasks) that are assigned to them. Cannot view the activity of any other users. </td></tr></tbody></table>

#### Common Role Configurations

* **Labelers** are often first added to an Organization as Org Members, added to relevant Projects as Project Members, and given access to the Label Stage by a Project Admin.
* **Internal Reviewers** are often first added to an Organization as Org Members and then added to relevant Projects as Project Admins, which gives them Project-wide Admin access.
* **External Reviewers** are often first added to an Organization as Org Members, added to relevant Projects as Project Members, and given access to any relevant Review Stages by a Project Admin.

### Inviting Members

You can view all the current members of your Organization inside the **Team Tab** on the left sidebar.&#x20;

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_team (1).png" alt=""><figcaption></figcaption></figure>

To invite a team member to your Organization, navigate to the Team Page, click on "Invite Member" and enter their email address and select their **Organization-level role** (i.e. either Org Admin or Org Member).&#x20;

<div data-full-width="false">

<figure><img src="../.gitbook/assets/Screenshot 2023-08-03 at 5.33.31 PM.png" alt=""><figcaption></figcaption></figure>

</div>

Once you invite them, they will receive an **email invitation** at the email address that you indicated.&#x20;

{% hint style="warning" %}
If you or a member of your team does not receive an email invitation, please check your spam folder. If the invitation is not in Spam, you can accept the invitation directly from the application by doing the following:

Navigate to [https://app.redbrickai.com/createaccount](https://app.redbrickai.com/createaccount) and fill in the relevant fields, being sure to use the email address to which the invitation was issued.

After logging in, you should be able to accept the invitation to your Organization.
{% endhint %}

Once a user has been invited to your Organization, you can invite specific users to individual Projects and manage their Project-level permissions.&#x20;

Each team member's Project-level permissions can be managed under the Workforce Tab of your Project Dashboard.&#x20;

{% hint style="success" %}
Assigning a Project Member to a particular Stage restricts their access to **only those Tasks that are currently in that specific Stage**. This restriction applies to both manual and automatic task assignment.&#x20;
{% endhint %}

Please see the short video below for an visual demonstration of how to limit a Project Member's access to a specific Stage. &#x20;

{% embed url="https://www.loom.com/share/7f3373ee787b422c868d4d2d92ac76d8" %}
