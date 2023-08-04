# SAML SSO

### Overview&#x20;

RedBrick AI is proud to offer SAML SSO for Enterprise-level clients, which allows your team to effortlessly access our platform using your trusted internal credentials for a seamless end-user experience.

Implementing SAML SSO for your Organization fundamentally alters the way that Users are added to and sign into your Organization on RedBrick AI.

Please see more detailed summaries of both of these processes below.

{% hint style="info" %}
If you'd like to implement SAML SSO for your organization, please reach out to us at support@redbrickai.com. We'll reach out to you directly to discuss the specific requirements of your integration given your company's existing security architecture.
{% endhint %}

### Inviting Users to a RedBrick Organization with SAML

After SAML has been configured for your Organization (and assuming you have the [proper permissions](../what-is-an-organization.md#organization-level-roles)), you can invite team members by first navigating to the Team Page.\
\
The "Invite Users" dialog will allow you to invite colleagues as either an Org Admin or an Org Member, as well as display a URL slug. This URL slug is unique to your Organization and is key to user sign-in, as detailed below.&#x20;

Simply enter the email address of the user you would like to invite to your RedBrick Organization, designate their privilege level and click "Send Invite".

<figure><img src="../../.gitbook/assets/invite-users-with-SAML.gif" alt=""><figcaption></figcaption></figure>

### Account Creation with SAML

After an Org Admin has extended an invitation, the user should receive a message in their email inbox containing a button that redirects the user to RedBrick AI to create an account (or, if they have already created an account, to sign in to your RedBrick Organization).

After clicking on the invitation link, the user will be prompted to confirm their Organization's unique URL slug.

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-04 at 1.01.29 PM.png" alt=""><figcaption></figcaption></figure>

After clicking on "Sign up with SSO", the user will be redirected to an external identity provider, where they will have to complete a successful login. If the login is successful, a RedBrick AI account will be generated for the user.

After a RedBrick AI account has been generated for the user, a confirmation code will be issued to their email address. Once the user enters that confirmation code into the necessary field, they will be able to join their team's RedBrick Organization and begin work.

### Signing In with SAML

Once a user has created an account on RedBrick AI and successfully joined an Organization that has SAML SSO enabled, they can easily sign in by clicking on "Sign in with SSO" on the login page.

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-04 at 3.22.28 PM.png" alt=""><figcaption></figcaption></figure>

After clicking on "Sign in with SSO", the user will be prompted to enter their Organization's unique URL slug. Enter the slug and click on "Sign in with SSO" to proceed to the RedBrick UI.

