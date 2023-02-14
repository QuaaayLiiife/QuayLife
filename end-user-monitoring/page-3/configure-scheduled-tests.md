# Configure Scheduled Tests

ThousandEyes users can create HTTP server tests and agent-to-server tests that run without user interaction at regularly scheduled intervals for as long as the Endpoint Agent is online, providing data from remote employees and smaller branch offices.

This article includes instructions for creating, modifying, and deleting scheduled tests, as well as reference information for the various configurable test settings.

* ThousandEyes Endpoint Agent software version 0.96 or later. Versions prior to 0.96 cannot run scheduled tests.
*   The users must have the required

    [permissions](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/getting-started-with-endpoint-agent#endpoint-agent-permissions)

    to create tests.

To create a scheduled test:

1.  2\.

    Click the **Add New Test** button.
2.  6\.

    **Optional:** Click the **Show Details** link and open the **Add Labels** drop-down list to add any test labels.
3.  7\.

    Click **Run Once** to run an instant test, click **Add New Test** to save the test, or click **Cancel** to discard the changes.

By default, the tests are assigned to the agent in the manner explained

[here](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/assign\_tests\_to\_agents)

.

### Manage Existing Scheduled Tests <a href="#manage-existing-scheduled-tests" id="manage-existing-scheduled-tests"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-59fb9644bf618cd0f82747f8842492802a0480a3%2Fproduct-documentation\_endpoint-agent\_configure\_scheduled\_tests\_2.png?alt=media)

The table shows the test name, test labels, test type, target URL/IP address, when the test was last modified, the number of agents assigned to the test in the last 24 hours, and whether the test is currently enabled or not.

#### Enable / Disable Scheduled Tests <a href="#enable-disable-scheduled-tests" id="enable-disable-scheduled-tests"></a>

To enable or disable an existing test:

1.  2\.

    Click the **Enabled** toggle switch to set the test to either enabled (blue) or disabled (dark gray).

If the toggle is grayed out, the test has no labels assigned it that match any available agents, and cannot be enabled. Update the agents to run the test in order to enable it.

#### Prioritise a Scheduled Test <a href="#prioritise-a-scheduled-test" id="prioritise-a-scheduled-test"></a>

By default, when scheduled tests are assigned to execution slots, they are prioritized as follow:

1.  1\.

    Tests which target specific machines
2.  2\.

    Tests which target specific labels

However, you can choose whether a scheduled test can override the default prioritisation plan.

To prioritise a scheduled test:

1.  2\.

    Click the **Prioritised** toggle switch to prioritise (blue) the test. You can set the test to default priority by toggling off (grey) the Priortised toggle.

### Configure an Existing Test <a href="#configure-an-existing-test" id="configure-an-existing-test"></a>

To configure an existing test:

1.  1\.

    From the

    [Endpoint Agents > Test Settings > Endpoint Tests](https://app.thousandeyes.com/endpoint/test-settings/?tab=tests)

    tab, identify the test that should be configured, either by scrolling down the list, searching for the test with the search function, or using the available filters to focus the list of tests shown.
2.  2\.

    Click the relevant row in the table to open the side panel.
3.  4\.

    Click **Run Once** to run an instant test, click **Save Test** to save the changes, or click **Cancel** to discard the changes.

### Duplicate an Existing Test <a href="#duplicate-an-existing-test" id="duplicate-an-existing-test"></a>

To create a duplicate of an existing label:

1.  1\.

    From the

    [Endpoint Agents > Test Settings > Endpoint Tests](https://app.thousandeyes.com/endpoint/test-settings/?tab=tests)

    tab, identify the test that should be configured, either by scrolling down the list, searching for the test with the search function, or using the available filters to focus the list of tests shown.
2.  2\.

    Click the three dots icon at the end of the test row.
3.  3\.

    Click **Duplicate**. The test configuration side panel will open with the duplicated test settings already configured.
4.  5\.

    Click **Run Once** to run an instant test, click **Add New Test** to save the test, or click **Cancel** to discard the changes.

To delete an existing Endpoint Agent test:

1.  1\.

    From the

    [Endpoint Agents > Test Settings > Endpoint Tests](https://app.thousandeyes.com/endpoint/test-settings/?tab=tests)

    tab, identify the test that should be configured, either by scrolling down the list, searching for the test with the search function, or using the available filters to focus the list of tests shown.
2.  2\.

    Click the three dots icon at the end of the test row.
3.  4\.

    Click **Delete** to confirm the change, or cancel to revert.
