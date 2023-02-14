# Alert Suppression Windows

The ThousandEyes platform provides Alert Suppression Windows to suppress alerting for tests during periods such as planned maintenance. Windows can be one-time events or recurring events to handle periodic occurrences such as monthly downtime for maintenance.

The Alert Suppression Window is displayed as a blue bar on the timeline of any test to which the Alert Suppression Window is assigned. Mousing over the bar displays the description:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-06f8266a3803783553e440b447b56c7ada948ed5%2Frelease-notes\_2015\_2015-03-04-release-notes-2.png?alt=media)

### Effects on Alerts and Notifications <a href="#effects-on-alerts-and-notifications" id="effects-on-alerts-and-notifications"></a>

During an Alert Suppression Window, data from tests assigned to the Window is not evaluated against Alert Rule criteria. Data that meets alerting conditions will not trigger an alert until the Alert Suppression Window has ended. Notifications (such as emails, Webhooks or PagerDuty integrations) which would normally occur will not occur during the Window. However, be aware of the following edge cases:

* If an Alert Rule's criteria require two or more rounds in a row to trigger, then no rounds within the Window can contribute to the consecutive rounds.
* If an Alert Rule's criteria require two or more Agents in the same round to trigger, it is possible for the Alert Suppression Window to start or end at a time within a round of data when some Agents running the test have gathered data but others have not. As a result, conditions that would normally trigger an Alert Rule do not trigger the Alert Rule at the edge of the Window. An example when this may happen is an Alert Suppression Window whose start or finish time ends in '5', and the Alert Suppression Window is assigned to tests which run at 2-minute intervals. The Alert Suppression Window may start before or end after only some of the Agents have collected data. Those Agents which have not collected data will not contribute to Alert Rule evaluation.
* If an Alert Rule is active at the beginning of an Alert Suppression Window, the Alert is not cleared once the Alert Suppression Window begins. Since no data is evaluated for alerts during the Alert Suppresion Window, the alert cannot be cleared until the Alert Suppression Window has ended, and data gathered which does not meet the Alert Rule criteria.

**IMPORTANT: The ThousandEyes platform runs on Universal Coordinated Time (UTC). Because UTC does not experience a period of Daylight Savings Time, the Alert Suppression Windows do not take into account Daylight Savings Time. If an Alert Suppression Window is scheduled prior to the beginning or end of Daylight Savings Time to run at a time after the change in Daylight Savings Time, the Window will be off by the amount of the time shift. Please check your scheduled Alert Suppression Windows prior to the beginning or end of Daylight Savings Time and make any necessary adjustments.**

Only tests to which an Alert Suppression Window is assigned are affected by an Alert Suppression Window. Other tests are not affected. Also, Notifications for non-test related events such Enterprise Agents going offline or online are not affected by an Alert Suppression Window.

Alert Suppression Windows can only be configured for Cloud and Enterprise Agent tests. Alert Suppression Windows for Endpoint Agent tests are not currently supported.

### Configuring Alert Suppression Windows <a href="#configuring-alert-suppression-windows" id="configuring-alert-suppression-windows"></a>

To configure an Alert Suppression Window, navigate to

[**Alerts > Alert Suppression**](https://app.thousandeyes.com/settings/asw/)

. Click **Add New Alert Suppression Window** to configure a new Window, or click an existing window's row to change settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bffb6f02200fa1752ef25d2d4e85f7d7c9e5d6f1%2Fproduct-documentation\_alerts\_alert-suppression-windows-2.png?alt=media)

1.  1\.

    **Name:** The name of the Alert Suppression Window.
2.  2\.

    **Tests:** Tests to which this Alert Suppression Window is assigned.
3.  3\.

    **Enabled:** Check this box to enable the Alert Suppression Window or uncheck the box to disable.
4.  4\.

    **Starts:** The start date and time of the Alert Suppression Window, and the time zone for the time. The start time of the Window must be at least 10 minutes ahead of the current time.
5.  5\.

    **Duration:** The length of time that the Alert Suppression Window will last.
6.  6\.

    **Repeat:** Repeat the Alert Suppression Window once per day, week, month or on a custom number of days, weeks or months. If month is chosen, text will be displayed indicating what day of the month the repetition will take place, based on the day selected in the **Starts** menu. Once a frequency is selected, the **End Repeat** menu will appear.
7.  7\.

    **End Repeat:** Select no end to the number of repetitions, a finite number of repetitions or a date on which to stop the repetition of the Window.
8.  8\.

    **Create New Window/Cancel:** Click the **Create New Window** button to save your configuration or click **Cancel** to exit without saving.
9.  9\.

    **Search:** Enter a text string to search for an Alert Suppression Window by name, in the table below.
10. 10\.

    Table of existing Windows: The table displays rows of previously configured windows. The table has the following columns:

    * **Name:** The name of the Alert Suppression Window.
    * **Next Schedule:** The date and time of the upcoming Window (if any). Note that a window may currently be active, but the next Window's date and time will be displayed.
    * **Duration:** The length of time that the Alert Suppression Window will last.
    * **Tests:** The number of tests to which this Alert Suppression Window is assigned.
    * **Status:** The status of the current Window. Statuses are:
      * Enabled: The Alert Suppression Window is configured and will become active at the next configured date and time.
      * Active: The Alert Suppression Window is currently in effect.
      * Ended: The last occurrence of the Alert Suppression Window has ended.

Configuration of Alert Suppression Windows requires the _Edit alert suppression windows_ permission, and viewing the windows requires the _View alert suppression windows_ permission.
