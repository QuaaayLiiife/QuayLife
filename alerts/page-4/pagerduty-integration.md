# PagerDuty Integration

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-81e70b7673a6b087dcab5349648cf62bf6e85999%2Fproduct-documentation\_alerts\_pagerduty-integration-1.png?alt=media)

In order to integrate with PagerDuty, you need the following components in place.

1.  2\.

    ThousandEyes alert rule(s)
2.  3\.

    A PagerDuty service (which is based on a PagerDuty escalation policy)

Think of a PagerDuty service as a destination for your alerts. Just as with an email notification, the alerts need to be sent somewhere: the reason you'd integrate into a system like PagerDuty allows you to manage notification destinations, repeat notifications, and escalation rules for each recipient of the alert.

If you don't have an Escalation Policy defined for your alerts coming from ThousandEyes, log in to PagerDuty and create an Escalation Policy. This defines how frequently users are notified, and who receives the notifications.

#### Create an Escalation Policy <a href="#create-an-escalation-policy" id="create-an-escalation-policy"></a>

On the top nav, click Escalation Policies, then on the upper right side of the page, click New Escalation Policy. In an escalation policy, you can define who gets notified, how frequently, and using which methods. Depending on the configuration of your team, you can configure an On-Call Schedule - which allows users to rotate through an on-call schedule, allowing handoffs of active incidents, or a user-based Escalation Policy. If you want to configure your Escalation Policy to use a schedule, create this schedule (Top Nav > On-Call Schedules) before attempting to create the Escalation policy.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-73a73aa3b474d10a8f2a09de97f1f74db93d91f1%2Fproduct-documentation\_alerts\_pagerduty-integration-2.png?alt=media)

1.  2\.

    Add users or on-call schedules to the policy
2.  3\.

    Determine how long before the alert gets escalated
3.  4\.

    Repeat steps 2-3 for escalations
4.  5\.

    Set repeat notifications until acknowledged
5.  6\.

    Save your Escalation policy

Once you have an escalation policy defined, you can configure a service which will accept notifications from ThousandEyes and begin the escalation policy.

#### Creating a Service Using ThousandEyes <a href="#creating-a-service-using-thousandeyes" id="creating-a-service-using-thousandeyes"></a>

There are two methods of PagerDuty service creation, but we'll only show you the ThousandEyes side here.

From ThousandEyes, under **Alerts > Alert Rules**, open the rule you wish to link to PagerDuty, then click the **Notifications** tab. Select **Edit Integrations**, then select **Add New Integration**, then select **PagerDuty** from the dropdown menu, and then **Add New PagerDuty service**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-481881a3fee610d65a8fc1c838fcd93b6cbbfbcf%2Fproduct-documentation\_alerts\_pagerduty-integration-3.PNG?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-060eee2b6cee1c6c87b8d83403ba1aeb21437568%2Fproduct-documentation\_alerts\_pagerduty-integration-4.PNG?alt=media)

This takes you to an authorization page on the PagerDuty site, which requests your username and password, then logs you in.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-124234440349a34505878da48e547114e01ddc13%2Fproduct-documentation\_alerts\_pagerduty-integration-5.png?alt=media)

Once you've authenticated and authorized the integration, you can select multiple existing PagerDuty services. **Note** You can only create integrations for services that have both alerts and incidents enabled in PagerDuty.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7b2a1a69642885da1bf3bcbfcdcee46e170d01f2%2Fproduct-documentation\_alerts\_pagerduty-integration-6.png?alt=media)

In the example below, we've created a new service based on a ThousandEyes test service policy and Dev App.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6e186b5e6bd4c7c8126d2d5e88b2419586c4146a%2Fproduct-documentation\_alerts\_pagerduty-integration-10.png?alt=media)

Finally, click **Connect**. You can ignore the warning about being "almost done". You're done, and alerts triggering on the basis of this alert rule will be routed to users in your escalation policy.

If you select multiple services, multiple integrations will be created on the ThousandEyes end. We will provide feedback on each integration as to whether they were successfully created. If you already have an integration with the selected service, we will prevent you from creating a duplicate. See the image below for an example:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-310afc7272fc128b75a64ddaa5de9bbb78d8ad74%2Fproduct-documentation\_alerts\_pagerduty-integration-11.png?alt=media)

### How the Integration Works <a href="#how-the-integration-works" id="how-the-integration-works"></a>

Once you've configured a PagerDuty service, and an alert is generated, the alert will trigger a new Incident in PagerDuty, which will follow the Escalation policy upon which the service is based. This escalation policy may:

* Notify through mobile push notification (iOS/Android)
* Notify by calling you and using Text to Speech

In most cases, the alert must be acknowledged, at which point the escalation policy stops. Users can add notes following an acknowledgement, and can clear the mark the alert as Resolved as required. If the alert rule conditions are no longer met by your test (or the alert rule is updated such that the conditions no longer meet the criteria of the alert), the alert rule is marked as cleared within PagerDuty via an incident update.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c1067f1a994d69af5c98c3cb99558902068c222e%2Fproduct-documentation\_alerts\_pagerduty-integration-7.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-70bdb46c6b4b2499ed69ccf02e00afcadcb6daff%2Fproduct-documentation\_alerts\_pagerduty-integration-8.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-82cd3353335a2ab6d8c49013f4e10d1ac7f7670a%2Fproduct-documentation\_alerts\_pagerduty-integration-9.png?alt=media)

#### Mapping of ThousandEyes Alert Severity to PagerDuty Incident Severity <a href="#mapping-of-thousandeyes-alert-severity-to-pagerduty-incident-severity" id="mapping-of-thousandeyes-alert-severity-to-pagerduty-incident-severity"></a>

Once you've configured a PagerDuty service and an alert is generated, the alert will trigger a new incident in PagerDuty with one of the following severity levels:

| ThousandEyes Alert Severity | PagerDuty Incident Severity |
| --------------------------- | --------------------------- |
| Info                        | Warning                     |
| Minor                       | Warning                     |
| Major                       | Error                       |
| Critical                    | Critical                    |

This mapping of the severity values from ThousandEyes alerts to PagerDuty incidents cannot be edited.
