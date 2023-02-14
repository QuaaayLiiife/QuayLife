# Setting Up Alert Rules for Internet Insights

Use the **Internet Insights** alert type to identify outages by provider and/or

[My Affected Tests](https://docs.thousandeyes.com/product-documentation/internet-insights/using-alerts-and-dashboards/my-affected-tests)

.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ccb98101759fa40ecb549d43a43088e0c6320e15%2Fsetting-up-alert-rules-for-int-001.png?alt=media)

To set up alerts for Internet Insights:

1.  1\.

    Go to **Alerts > Alert Rules**.
2.  2\.

    On the **Internet Insights** tab, click **Add New Alert Rule**.
3.  3\.

    In the dialog that opens, configure the alert rule on the **Settings** tab.

    * **Affected Tests** can be any test owned by any account group within your organization, or choose specific tests.
4.  4\.

    Use **Alert Conditions** to specify thresholds. Options are:

    * **Affected Applications**: Choose from a list to include or exclude. You must have licensed the corresponding application package in order to receive alerts on those specific applications.
    * **Affected Domains**: Enter a domain to include or exclude, for example google.com.
    * **Affected Servers Count**: Specify a threshold.
    * **Affected Tests Count**: Specify a threshold.
    * **ASN**: Enter an Autonomous System Network (ASN) number to include or exclude.
    * **Outage Error Type**: Choose error types to include or exclude (DNS, HTTP, Network, or SSL options).
    * **Server Locations**: Choose from a list of server locations to include or exclude.
    * **Server Locations Count**: Specify a minimum number of affected server locations.

You don’t have to associate Internet Insights alert rules explicitly with a test. The rule is operational as soon as it is saved.
