# Configure Automated Session Tests

This article includes instructions for creating, modifying, and deleting automated session tests, as well as reference information for the various configurable test settings.

* ThousandEyes Endpoint Agent software version 1.100 or later.
*   The users must have the required

    [permissions](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/getting-started-with-endpoint-agent#endpoint-agent-permissions)

    to create tests.

### Create an Automated Session Test <a href="#create-an-automated-session-test" id="create-an-automated-session-test"></a>

To create an automated session test:

1.  2\.

    Click the **Add New Test** button.
2.  5\.

    Click **Add New Test** to save the test, or click **Cancel** to discard the changes.

### Manage Existing Automated Session Tests <a href="#manage-existing-automated-session-tests" id="manage-existing-automated-session-tests"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d3bf80c129495070a2309ad2c02efc0093df6b31%2Fproduct-documentation\_end-user-monitoring\_dynamic-app-test\_configure-dynamic-app-tests-3.png?alt=media)

The table shows the test name, the corresponding application, the number of agents assigned to the test in the last 24 hours, and whether the test is currently enabled or not.

#### Enable / Disable Automated Session Tests <a href="#enable-disable-automated-session-tests" id="enable-disable-automated-session-tests"></a>

To enable or disable an existing test:

1.  2\.

    Click the **Enabled** toggle switch to set the test to either enabled (blue) or disabled (dark gray).

If the toggle is grayed out, the test has no labels assigned it that match any available agents, and cannot be enabled. Update the agents to run the test in order to enable it.

#### Prioritise an Automated Session Test <a href="#prioritise-an-automated-session-test" id="prioritise-an-automated-session-test"></a>

By default, the tests are assigned to the agent in the manner explained

[here](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/assign\_tests\_to\_agents)

.

However, you can choose whether an automated session test can override the default prioritisation plan.

To prioritise an automated session test:

1.  2\.

    Click the **Prioritised** toggle switch to prioritise (blue) the test.

You can set the test to default priority by toggling off (grey) the **Priortised** toggle.

### Configure an Existing Test <a href="#configure-an-existing-test" id="configure-an-existing-test"></a>

To configure an existing test:

1.  2\.

    Click the relevant row in the table to open the side panel.
2.  4\.

    Click **Save Test** to save the changes, or click **Cancel** to discard the changes.

### Duplicate an Existing Test <a href="#duplicate-an-existing-test" id="duplicate-an-existing-test"></a>

To create a duplicate of an existing test:

1.  2\.

    Click the three dots icon at the end of the test row.
2.  3\.

    Click **Duplicate**. The test configuration side panel will open with the duplicated test settings already configured.
3.  5\.

    Click **Add New Test** to save the test, or click **Cancel** to discard the changes.

To delete an existing Endpoint Agent test:

1.  2\.

    Click the three dots icon at the end of the test row.
2.  4\.

    Click **Delete** to confirm the change, or cancel to revert.
