# How to Configure SCIM with Okta

ThousandEyes users can be added, deleted and modified using SCIM 2.0 and 1.1 compatible identity providers, dramatically decreasing time to provision users into ThousandEyes. This document describes the integration between identity provider Okta and ThousandEyes.

This integration has been fully tested by Okta and ThousandEyes but it's currently not available for all Okta organizations. If you wish to try user provisioning on ThousandEyes through Okta, please reach us at \[email protected]

To perform configuration in ThousandEyes, a user having a role with the following permissions is required:

* User provisioning (creation)

Group information or other user attributes cannot be translated into Account Groups, Roles or any other ThousandEyes structure.

To begin, open Okta and click on the **Admin** button on the top right:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f70c1937c49ce76bd6a42cbcae6b1a1150e90703%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-1.png?alt=media)

Once in the dashboard, click on the Applications menu, and then on the Applications sub menu:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c3a00b403373764b4ef77df073fbec01e72d5855%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-2.png?alt=media)

Click on **Add Application**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-95e0bba539b5b3cd8c17d7178f2604800139cc6b%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-3.png?alt=media)

Type “ThousandEyes” in the search bar, then click on the **Add** button of the listed ThousandEyes App:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c8cf09c0b9c951b4c2ec06c7ab80f67746826049%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-4.png?alt=media)

Type in a Name for your Application, then click Next:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9c873622cf832b693df4e7671e9e09012f625239%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-5.png?alt=media)

Under “Application username format” select in the drop down menu the “Email” option.

If you wish to configure SAML 2.0 SSO click on the “View Setup Instructions” button and follow the steps on the following page to finish SSO configuration in ThousandEyes. Otherwise, you can ignore this part of the configuration and click **Next**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-da8e532845e5c0810a92f390430dcb3ee056f7da%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-6.png?alt=media)

In the provisioning settings, check the **Enable provisioning features** box:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1836e851f86203406923e3a04d96ac1dac4a735f%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-7.png?alt=media)

Now enter the following information in the “API Credentials” form:

* **Username**: ThousandEyes username (email) with a role having permissions to create accounts
*   **Password**: API token of the selected ThousandEyes user (found at **Account Settings > Users and Roles**)

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5bf4531452a2682ab9cb8ce164dfa2d2131c281c%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-8.png?alt=media)

Click on **Test API credentials** to make sure the API token and username were entered correctly. This should return a message similar to this one:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b40762ba02c7a4feb034fd80cda72acb38cc7306%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-9.png?alt=media)

If an error is present, verify that the selected user has the permissions stated in the Requirements section of this document. If the issues persist, please contact ThousandEyes Customer Success Center (\[email protected]) to assist.

Under “Provisioning Features” select the following options:

* **Schedule Import** - Select a time
*   **Okta username format** - Email address

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4bd38b5d61c6eb3281392a5ed70c07fb154366f1%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-10.png?alt=media)
* **Update User Attributes** - Enabled
*   **Deactivate Users** - Enabled

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-aa8de6ba8e02f5d8345fbe1d24ae00f61f384ef9%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-11.png?alt=media)

Once this is completed, click on **Next**.

Optional: Add users now so they are integrated to the App. Otherwise just click on “Next”

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-10d84f048bcb1c67840e60e2c5f29fc045b7441a%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-12.png?alt=media)

And click on “Done” to finish the configuration:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9a44aef16967f640e235bda8695c03911dcd799c%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-13.png?alt=media)

At this point of time, setup of SCIM with ThousandEyes is complete.

### Testing the SCIM Integration <a href="#testing-the-scim-integration" id="testing-the-scim-integration"></a>

To verify that the integration is working, add a user to the Application.

From the home page, go to Applications > Applications

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4bf0c3962490c7f9f3532c0f538c6fc83dcee92d%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-22.png?alt=media)

Then click in the newly added app:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7de69c6cf358a9c02970dfe9a35f4c4944e67a09%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-15.png?alt=media\&token=60736ba5-0e0f-4afd-9cb9-100ac055af0a)

Now click on **Assign to People:**

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4179a98c87d43dcfad6c9cebe6821ffcfec79e4f%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-16.png?alt=media)

Select the people you want to be pushed to ThousandEyes as users by clicking on the **Assign** button next to them:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d97557649a4c6e63170dbfa48651538ac1fe903d%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-17.png?alt=media)

Then click on **Save and Go Back** after reviewing the user information:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d6711ec83b029bc03eb3f4c4abdd355f3dae8fd4%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-18.png?alt=media)

Repeat this for all users you want to push to ThousandEyes. When done, click on **Done**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b3dadd633acf8604f971780bbbe638dec52cafed%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-19.png?alt=media)

If the User ID (email) is already registered with ThousandEyes, then the new access, permissions and roles will be configured accordingly on this user, matching what was configured in the “SCIM Settings” section of your organization’s Security and Authentication settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e0baed975480e9841c36a1b451ad6f596e0ca523%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-20.png?alt=media)

If the user doesn’t exist, it will be created in ThousandEyes and no registration or activation will be required from the newly created user.

Within ThousandEyes, the user should be visible shortly after it was associated with the service from Okta. To validate this, go to the Users section within Account Settings and verify the newly added user is present there:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f3d5582879bf0988a5bb856d86923e0285f18a6f%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-21.png?alt=media)

To delete a user, open the Application from Okta,

From the home page, go to Applications > Applications

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4bf0c3962490c7f9f3532c0f538c6fc83dcee92d%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-22.png?alt=media)

Then click in the newly added app:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7de69c6cf358a9c02970dfe9a35f4c4944e67a09%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-15.png?alt=media\&token=60736ba5-0e0f-4afd-9cb9-100ac055af0a)

Now click on the “X” button next to the user you want to delete:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e640d6ce879b9d4d45f01b491d802a62d5305de8%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-24.png?alt=media)

Confirm the prompt to verify that the user will be unassigned from the Application:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bd4b8326068173b99c6b26e5eb56106ff9067f0d%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-25.png?alt=media)

The user should be shortly deleted from ThousandEyes. This is also verifiable within the Users section within Account Settings

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8f6abb5ed20d954750995ab78c9241450a0df48f%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-okta-26.png?alt=media)
