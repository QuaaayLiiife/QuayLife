# Transaction Test Migration Workflow

ThousandEyes has added a new migration workflow to assist users in converting older-generation transaction (classic) tests to the more powerful, JavaScript-based current generation of transaction tests. This section covers how to migrate a test, the limitations of the workflow, and outlines the parts of the conversion that require manual configuration.

**Important:** The workflow is only needed by users with existing transaction (classic) tests.

The migration workflow takes an existing transaction (classic) test and creates a new transaction test with the same exact name that replicates the configuration as closely as possible. The new test can then be reviewed and adjusted as necessary before saving.

Transaction (classic) tests that have not been migrated yet can be identified by the warning icon beside the test type in the **Test Settings** page:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-53b0730ecc8a03838923bc66e427d6782c297bbe%2Frelease-notes\_2020-05-12\_feature-transaction-workfow-one.png?alt=media)

The migration workflow requires that:

* The workflow is enabled for the account.
* The transaction (classic) test is owned by the account.
* The user has the required permissions to create/edit tests on the account.

**Important:** The migration workflow will not be visible if the user does not have the necessary permissions, if the test is owned by a different account and shared with the current one, or if the workflow has not yet been enabled for the account. If you do not have access to the workflow, but have transaction (classic) tests you wish to migrate, contact Customer Support.

Every configuration option in a transaction (classic) test does not have a direct equivalent in the new generation of tests. ThousandEyes recommends understanding the goal of the original test before migrating, so that the intent of the test can be replicated where exact configuration options cannot be.

The sections below outline the parts of the test, which parts require manual configuration, and the limitations of the workflow.

**Basic and Advanced Configuration**

The basic configuration options are migrated over directly. Any advanced configuration options that have a direct equivalent will be migrated over, while any configuration options that are available in the new test type but not available to transaction (classic) tests will be set to the default value.

All labels applied to the original test will also be applied to the new test.

**Dashboard and Report Widgets**

Dashboard and report widgets are not migrated automatically to the new test, as they are configured for a specific test type. Once the test is migrated, users will need to configure each dashboard and report for the new test.

Alert rules are not migrated automatically to the new test, as each alert rule is written for a specific test type. Once the test is migrated, users will need to recreate each alert rule for the new test.

**Important:** There is not a direct equivalent for every transaction (classic) test alert rule for the new transaction test type. ThousandEyes recommends reviewing the goal of the original alert rules so that the intent can be recreated in the new test. See

[How Alerts Work](https://github.com/thousandeyes/docs/blob/prod/product-documentation/alerts/how-alerts-work.md)

for details on configuring transaction test alert rules.

**Step-Based Configuration and Markers**

In step-based transaction (classic) tests, the step timing for each test round is collected and made available as metrics that are visible in the test view, dashboards, reports, and as alert rule conditions. The new transaction tests are not step-based, and instead collect sub-transaction timings with more flexibility using markers.

To help with manual configuration, each step from the original test has been added to the script wrapped with

[markers](https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/transaction-scripting-reference.md#markers)

in an effort to maintain parity with the original test as much as possible.

Each marker must be unique in new transaction tests. If duplicate step names exist in the transaction (classic) test, the step number will be appended to the marker to ensure all markers are unique in the migrated test.

The new transaction test type allows users to build tests that can track the timing of specific segments, rather than the step-based model that recorded timings for every step. ThousandEyes recommends reviewing each marker to determine whether it is still necessary in order to decrease the amount of extraneous data recorded.

The new transaction test type allows sensitive text to be encrypted in the credential repository and referenced in the transaction test script.

The previous-generation transaction (classic) tests encrypted all text input, regardless of sensitivity. As there is no surefire way of differentiating between sensitive and non-sensitive text input when migrating the test, all data that is configured to be input (usernames, passwords, emails etc) in the original test will be added to the credential repository and referenced in the script. This ensures tests should work out of the box while ensuring there is no sensitive text hard-coded into the converted script.

When reviewing the script post-migration, the non-sensitive data can be hard-coded into the script and removed from the credential repository as necessary.

**Important:** The auto-generated credential names may be long and difficult to read and use. ThousandEyes recommends reviewing them, and renaming them with shorter and more accurate names where necessary.

Two examples of how duplicate credentials can be created are listed below:

**Multiple transaction (classic) tests that use the same encrypted values are migrated.**

Each migrated test will create new entries in the credential repository for any input text. If multiple tests use the same credentials, ThousandEyes recommends removing the duplicate values and using the same credential in each test.

**A transaction (classic) test is migrated twice.**

Currently, there is a 1x1 mapping between transaction (classic) tests and the new transaction tests. If a transaction (classic) test is migrated, it can't be migrated again without deleting the original migrated test. Most users will not need to migrate tests a second time, as any troubleshooting will be done in the original migrated test.

However, an edge case exists where:

1.  1\.

    Transaction (classic) test "Example TX Test" is migrated and saved.
2.  2\.

    The credential name "Example TX Test-12345-3-Enter password" used in "Example TX Test" is renamed "te-credential\_name-password".
3.  3\.

    "Example TX Test" is migrated a second time. The second test is called "Example TX Test 2".

In this example, the credential repository would have duplicate credentials, as the first set of credentials (renamed "te-alias-password") would not be removed from the repository, and will not be applied to "Example TX Test 2".

ThousandEyes recommends removing unnecessary and duplicate credentials from the repository to improve usability.

### Migrate a Transaction (Classic) Test <a href="#migrate-a-transaction-classic-test" id="migrate-a-transaction-classic-test"></a>

1.  1\.

    Select the relevant test from the **Test Settings** page to expand the window.
2.  2\.

    You will be redirected to the **Add New Test** window, populated with an auto-generated configuration for an equivalent transaction test. The transaction steps will be translated to JavaScript and added to the **Basic Configuration** tab.
3.  3\.

    Review the new transaction test, and edit as necessary.

    **Warning:** Several parts of the original transaction (classic) test, including the alert rules, will not be migrated. See the

    [Manual Configuration](https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/transaction-test-migration-workflow.md#manual-configuration)

    section for more information.

    **Important:** During the automated translation process, instances may be identified where small changes need to be made to the resulting script in order for it to run correctly. Wherever this is the case, comments will be included in the translated script describing the changes that may be required. In many instances, no modifications will be necessary. An instant test can be run to confirm whether the test work as is or not. Once any issues have been resolved, the related comments can be deleted.
4.  4\.

    Run an instant test by clicking **Run Once** to validate the migrated script.

    **Note:** If the test fails, the ThousandEyes recorder IDE can be used to review the test as it runs to identify the issues. However, if you are troubleshooting / modifying the code in the recorder IDE, ThousandEyes recommends copying and pasting the edited script back into the "Add New Test" form, rather than using the **Export to ThousandEyes** button.
5.  5\.

    Click **Create New Test** to save the migrated test.

#### Impacted Alerts, Dashboards, and Reports <a href="#impacted-alerts-dashboards-and-reports" id="impacted-alerts-dashboards-and-reports"></a>

Once the new test has been created, a pop-up modal will appear with a list of dashboards, reports, and alerts that are impacted by the original transaction (classic) test, and will need to be updated for the new test. A link is provided to each dashboard and report from the modal.

**Note**: Alerts are not linked from the modal, and will need to be searched by name manually.

If the modal is closed, or you want to review the list of impacted alerts, dashboards, and reports:

1.  1\.

    Navigate to the **Cloud and Enterprise Agents -> Test Settings** page.
2.  2\.

    Click on the relevant transaction (classic) test to expand the view.
3.  3\.

    Click the **View Next Steps** button at the top.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-52be6157415d0d8f002af574a7c704fcc3503d36%2Fproduct-documentation\_tests\_transaction-test-migration-workflow-2.png?alt=media)

    ​

In some instances, you may want to migrate the test a second time. To migrate a test that has already been migrated before:

1.  1\.

    Navigate to the **Cloud and Enterprise Agents -> Test Settings** page.
2.  2\.

    Click on the relevant transaction (classic) test to expand the view.
3.  3\.

    Click the **Migrate to New Transaction Test** button at the bottom.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dbaf9a36880e370834808dd5c82cf4cfa2fbdb2e%2Fproduct-documentation\_tests\_transaction-test-migration-workflow-3.png?alt=media)

    ​

**After migrating the test, will the original test be automatically disabled?**

No. The two tests should be run in parallel until alerts, reports, and dashboards are set up for the new test and you are satisfied with the new test's performance. Once the new test is performing well, the old test should be disabled.

**Warning:** Disabling a transaction (classic) test before setting up alerts, reports, and dashboards on the new test may result in a gap in your monitoring ability related to the original test.

**What happens to transaction (classic) test data after the test is disabled?**
