# 2 Sending ThousandEyes Alerts to AppDynamics

Another powerful way to integrate ThousandEyes and AppDynamics is to send ThousandEyes alerts to AppDynamics.

### Native Alerts Integration <a href="#native-alerts-integration" id="native-alerts-integration"></a>

First, set up ThousandEyes to send its alerts to AppDynamics. See the native

[alerts integration](broken-reference)

.

### Viewing ThousandEyes Alerts in the Application Dashboard <a href="#viewing-thousandeyes-alerts-in-the-application-dashboard" id="viewing-thousandeyes-alerts-in-the-application-dashboard"></a>

ThousandEyes alerts are displayed in AppDynamics as _custom events_. Any alerts that ThousandEyes generates about an application that AppDynamics is monitoring appear under the application in the top right corner:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cef14086267299315bd958bb99f5914918609591%2Fmonitoring-guides\_appdynamics\_integration-alerts-1.png?alt=media)

To view the custom events, do the following within AppDynamics:

1.  1\.

    The **Events** view appears, filtered by custom event.
2.  2\.

    Scan the **Events** view for any ThousandEyes alerts generated for that application.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-54e0018e69a46227fa1bb83d2985280442059edd%2Fmonitoring-guides\_appdynamics\_integration-alerts-2.png?alt=media)

    ​
3.  3\.

    Double-click one of the events.

    Details of the alert display, including a link back to the alert in ThousandEyes platform.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-40c08681fa3957dd50c501d2456007582533416c%2Fmonitoring-guides\_appdynamics\_integration-alerts-3.png?alt=media)

    ​

### Filtering on ThousandEyes Alerts <a href="#filtering-on-thousandeyes-alerts" id="filtering-on-thousandeyes-alerts"></a>

If you are ingesting alerts into AppDynamics from various sources, you may want to filter on ThousandEyes alerts only.

1.  1\.

    Navigate to the **Add Custom Event Filter** dialog.

There are several places in AppDynamics where you can add custom event filters. For example, **Application > Events > Add Criteria > Custom Events**.

1.  1\.

    In the **Custom Event Type** field, enter **ThousandEyesAlert**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6ae7fee6424a97265e60369d826477ec325bc54e%2Fmonitoring-guides\_appdynamics\_integration-alerts-4.png?alt=media)

    ​
2.  2\.

    To further refine your filtering, you can click **Add Property** and filter on any of the following properties:

    | Property Name  | Definition                                                                                                                                                                                                                                                      |
    | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | **alertType**  | Possible values include **BrowserBot**, **Http**, **Network**, **OneWayNetwork**, **Voice**, **DnspDomain**, **DnspNameServer**, **DnsServer**, **DnsTrace**, **Dnssec**, **Transaction**, **WebTransaction**, **Bgp**, **PathTrace**, **Ftp**, and **Sip**\*\* |
    | **testName**   | The name of the ThousandEyes test that is generating the alert.                                                                                                                                                                                                 |
    | **alertState** | **TRIGGER** or **CLEAR**                                                                                                                                                                                                                                        |
    | **scope**      | The number of agents affected.                                                                                                                                                                                                                                  |
    | **ruleName**   | The name of the ThousandEyes alert rule that has been triggered.                                                                                                                                                                                                |
    | **alertId**    | The unique ID of the alert.                                                                                                                                                                                                                                     |
    | **target**     | The URL that the test is set to.                                                                                                                                                                                                                                |

### Viewing ThousandEyes Alerts in AppDynamics Dashboards <a href="#viewing-thousandeyes-alerts-in-appdynamics-dashboards" id="viewing-thousandeyes-alerts-in-appdynamics-dashboards"></a>

To have ThousandEyes alerts appear in AppDynamics dashboards as overlays on metrics widgets, do the following:

1.  1\.

    Navigate to the dashboard widget and click to edit it.
2.  2\.

    In the **Edit Widget** dialog, find the **Events** section and select the **Show Events** option.
3.  3\.

    Ensure that the **Data Source** field shows the name of the application you want to show alerts about.
4.  4\.

    Select **Event Types: Custom**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f8d2148c905a2edd759ee757a07a610b7c5bf9b5%2Fmonitoring-guides\_appdynamics\_integration-alerts-6.png?alt=media)

    ​

#### Health Rules & Events Widgets <a href="#health-rules-and-events-widgets" id="health-rules-and-events-widgets"></a>

ThousandEyes alerts can also be displayed in the **Health Rules & Events** widgets, in both list and timeline view.

1.  2\.

    In the **Add Widget** dialog, select **Health Rules & Events > Event List**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6861392034584c86632a237e5f1d3c29f797bd29%2Fmonitoring-guides\_appdynamics\_integration-alerts-7.png?alt=media)

    ​
2.  3\.

    Select the data source (typically, the application you are monitoring).
3.  4\.

    Select **Add Criteria > Custom Events**.

### Using ThousandEyes Alerts in AppDynamics Policies <a href="#using-thousandeyes-alerts-in-appdynamics-policies" id="using-thousandeyes-alerts-in-appdynamics-policies"></a>

You can use ThousandEyes alerts to create policies that combine AppDynamics and ThousandEyes alerts. For example, you might create a policy that triggers when both a ThousandEyes network alert occurs as well as an AppDynamics slow application response time alert.

1.  1\.

    In the **Alert & Respond** section, select **Policies > Create**.
2.  2\.

    In the **Edit Policy** dialog, select **Custom Events**.
3.  3\.

    In the **Add Custom Event Filter** dialog, in the **Custom Event Type** field, enter **ThousandEyesAlert**.
4.  4\.

    Set property filters for **type** as **Network** and **alertState** as **TRIGGER**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-efed11b4ce949e51103661d9cf1979b50db66534%2Fmonitoring-guides\_appdynamics\_integration-alerts-8.png?alt=media)

    ​
5.  5\.

    Now select other conditions, such as **Slow Transactions**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-26259b41628c4aca1a7fb337ef6f4467a9b47229%2Fmonitoring-guides\_appdynamics\_integration-alerts-9.png?alt=media)

    ​
