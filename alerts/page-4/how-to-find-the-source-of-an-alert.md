# How to Find the Source of an Alert

This article describes the steps for tracking down what triggered an alert. To understand how alerts work, see

[How Alerts Work](broken-reference)

.

If you receive an alert from the ThousandEyes platform and you are trying to understand the root cause, follow the steps below to interpret what thresholds triggered the alert.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-38fbfbd95b81822f26f5c61e4611cb3ae3ab5bf8%2Fproduct-documentation\_alerts\_findsource-of-an-alert-1.png?alt=media)

1.  1\.

    When you receive an alert from the ThousandEyes platform, go to **Alerts > Alert List** in the platform.
2.  2\.

    Use the search box to find a specific alert by Alert ID or Name.
3.  3\.

    Having located the alert, find the **Test Name** column to see the test that is associated with the alert rule that was triggered.

    You can also see related metrics that help show why this alert rule was triggered.
4.  4\.

    Once you have the name of the test, go to **Cloud & Enterprise Agents > Test Settings** to see how that test is configured.
5.  5\.

    In the test's row, click the stack icon to view the test results. The test results offer a timeline view of the alert activity.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6ebd9dc807449d28a841eebdc6d443254ad2e916%2Fproduct-documentation\_alerts\_findsource-of-an-alert-2.png?alt=media)

If an alert is throwing notifications that exceed your operational requirements, you can adjust the alert condition thresholds.

1.  1\.

    Go to **Alerts > Alert Rules**.
2.  2\.

    Select the name of the alert rule that you want to adjust.
3.  3\.

    On the **Settings** tab, in the **Alert Conditions** section, review the current thresholds.
4.  4\.

    Make changes to these settings to reduce the frequency of alerts, according to your requirements.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-21ae393b86056daf8ca98e690fa0c7d13bbd8de8%2Fproduct-documentation\_alerts\_findsource-of-an-alert-3.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7c5a7f8fbb7a2dd98342d5d8adae56ec3467433e%2Fproduct-documentation\_alerts\_findsource-of-an-alert-4.png?alt=media)

After you adjust a noisy alert to meet your service-level expectations, the alert should begin to clear. An active alert that clears is moved to the **Alert History** tab. To view cleared alerts, go to **Alerts > Alert List > Alert History**.
