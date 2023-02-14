# Creating a Page Load Test

To create a ThousandEyes page load test, check with your Organization Admin to make sure you have permissions to create and edit test configurations. Use a ThousandEyes Cloud or Enterprise Agent, as you cannot run page load tests from an Endpoint Agent.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1a061d46dab6e8b0c4553350b48b6e203436edcd%2Fproduct-documentation\_browser-synthetics\_create-page-load-test.png?alt=media)

1.  1\.

    On the ThousandEyes platform, go to **Cloud & Enterprise Agents > Test Settings** and click **Add New Test**. If you don’t see this button, check that you have permission to create and edit test configurations.
2.  2\.

    On the Basic Configuration tab:

    * Choose **Web** as the Layer and **Page Load** as the Test Type.
    * Specify the URL, domain name, or IP address of the destination you want to test.
    * Select at least one Cloud or Enterprise Agent.
    * For the rest of the settings, you can accept the defaults if you want to get started quickly.
3.  3\.

    The **Advanced Settings** tab has additional options, with pre-configured defaults.
4.  4\.

    Click **Run Once** to make sure that the test works and doesn’t show any test configuration errors. You might have to wait a minute or two before test results display in a new browser tab.
5.  5\.

    Click **Create New Test** to save and begin running the new page load test immediately.
6.  6\.

    Go to **Cloud & Enterprise Agents** > **Views** to see test results. As the test continues to run, the data will reflect recent test history over time.

The minimum viable test configuration would be to set up a page load test for a public page such as Wikipedia, accept the defaults, and run it from a Cloud Agent. Cloud Agents are managed by ThousandEyes and are already available in locations around the globe.

For a complete list of test configuration options for web layer tests including the page load test, see

[Working with Test Settings](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/working-with-test-settings#web-layer-tests)

.
