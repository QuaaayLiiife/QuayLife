# Dashboard Sharing and Snapshots

Dashboard snapshots represent a specific time range of the dashboard’s data. Snapshots can be scheduled at regular intervals and automatically emailed to a list of recipients. You have the option to anonymize data when creating the snapshot.

You must be a ThousandEyes customer in order to create snapshots and share links of your own data. All ThousandEyes internal users, regardless of their function, are restricted from creating snapshots of customer data.

Dashboard data can also be shared through embedded widgets, which allow a dashboard's widgets to be included in customer web pages such as kiosk displays or network operations center dashboards. For more information on embedded dashboard widgets, see

[Embedding Dashboard Widgets in External Web Sites](broken-reference)

.

Snapshots can be created on demand, or created automatically according to a schedule. You can share snapshots with people outside your organization, whereas sharing a dashboard directly can only be done within your organization, with other ThousandEyes users who have access to the ThousandEyes platform.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0fd6dd7c0e054294162d6f515eb2186dfdacf94b%2Fdashboard-snapshot-menu.png?alt=media)

#### Working with Dashboard Snapshots <a href="#working-with-dashboard-snapshots" id="working-with-dashboard-snapshots"></a>

To view existing snapshots, click the Snapshot camera icon on the **Dashboards** page and choose either **All Snapshots** or **Related Snapshots**.

A pane appears with a list of the latest snapshots of each dashboard. If you are looking for a history of the snapshots associated with a specific dashboard, open that specific dashboard and then click the Snapshot icon. Snapshots created from a schedule have a watch icon next to the snapshot name.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-71a8ad643b5e2fd85a16103bf6a2bedf65b3400e%2Fdashboard-snapshot-pane.png?alt=media)

To share a link to a snapshot after creating the snapshot, right-click its entry and choose Copy Link Address from your browser right-click menu. The link will work if the snapshot has link sharing turned on. Link sharing is something you can change anytime by opening the snapshot and toggling it on or off. Use link sharing only if people outside your organization need to see it, for example, a third-party provider or ISP.

The Snapshot screen looks just like the regular dashboard, except that the upper right has an Exit Snapshot button.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-48d50c2e8a47e38743762bcc4bcb2f80fb8b0390%2Fdashboard-snapshot-screen.png?alt=media)

Here are the things you can do with dashboard snapshots:

* To save a snapshot as a file to your drive, open the snapshot and then use the Download icon and save the snapshot as a PDF file.
* To delete a snapshot, open the snapshot and click the Gear icon, then choose Delete Snapshot.
* You cannot edit an existing snapshot, other than to turn Link Sharing on and off.

When creating a new dashboard using the **New from this Dashboard** link, the newly created dashboard will not inherit the schedule for creating snapshots from the original dashboard.

#### Creating a New Dashboard Snapshot <a href="#creating-a-new-dashboard-snapshot" id="creating-a-new-dashboard-snapshot"></a>

To create an on-demand dashboard snapshot, select the desired dashboard in the Dashboard name pull-down on the Dashboards page. Then select the **Snapshot > Save a Snapshot** link from the Dashboards page. The **Save a Snapshot** side pane will appear. The dialog allows you to name the snapshot. The current date range in the dashboard date selector's To and From fields will be used to select the data in the snapshot. Options to anonymize data that can reveal a user's identity and creating a public share link are also available here.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4651eb9682f8028c0624dddba10da73b3b3b2ba7%2Fdashboard-snapshot-menu-save.png?alt=media)

When you save a snapshot, it can take a moment or two for the data to be generated. When the snapshot is ready, you’ll see a notification as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-36c23671fca38c97286feb25ea4c97ce52c06556%2Fdashboard-snapshot-notifications.png?alt=media)

#### Scheduling a Recurring Snapshot <a href="#scheduling-a-recurring-snapshot" id="scheduling-a-recurring-snapshot"></a>

Dashboard snapshots can be automatically generated at periodic intervals, such as each week or month. To schedule a recurring snapshot of a particular dashboard, open that dashboard, click the Snapshot camera icon, and choose Schedule a Snapshot.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-69c2de03af65236f099c87769e03b020c63267c2%2Fdashboard-snapshot-schedule.png?alt=media)

The following settings are available:

* **Snapshot Name:** Enter a name for the snapshot, which will appear in the listing under Dashboards > Dashboard Snapshots.
* **Repeat Interval:** Select the frequency with which to create snapshots. You may select from the following values:
  * None: Creates a single dashboard at the specified time.
  * Custom: Allows you to select an integer number of days, weeks or months.
* **Timezone:** Select the desired timezone. Note that the scheduled task runs at the time 0:00 on the hour within the selected timezone. If you want to run the scheduled task at a time other than 0:00 local time, select a different timezone. The menu shows the number of hours difference as well as the local time, so you'll know when the snapsot gets generated before saving your changes.
* **Next Repeat On:** Shows the time of the next scheduled snapshot.
* **Contains:** Select the number of days or weeks of data that the snapshot will cover, going back from the creation date of the snapshot.
* **Emails:** Displays addresses to which the ThousandEyes platform will email each snapshot. The recipients on the email list will receive an HTML-formatted version of the Snapshot and a link to the snapshot in the ThousandEyes platform, once the new snapshot is generated. Add addresses using the **Edit Emails** link.
* **Auto Share Snapshots:** When enabled, the dashboard snapshots will automatically be shared via a public link (see **Sharing Report Snapshots**, below). The link will be included in email if the Subscriber Emails (above) is configured. You can stop sharing the existing dashboard snapshots at any time. To stop automatic creation of the dashboard snapshots, uncheck the **Auto Share Snapshots** box.
* **Anonymize data that identifies users:** All data that could reveal user's identity are anonymized.
* **Include a PDF attachment of the Dashboard:** Attaches a PDF version of the dashboard snapshot when sending out dashboard snapshot notification emails.

A dashboard with an associated snapshot schedule will have a watch icon beside its name in the Dashboard name pull-down menu.

To remove the scheduled creation from a dashboard, select the schedule, select the desired dashboard in the Dashboard name pull-down on the **Dashboards** page, then select **Snapshot > Cancel Schedule** link.

**Note:** Changing the dashboard layout that generated a scheduled snapshot will not change existing snapshots. Only future snapshots will be affected by changes to the dashboard layout.

#### Downloading a Dashboard Snapshot <a href="#downloading-a-dashboard-snapshot" id="downloading-a-dashboard-snapshot"></a>

You don’t have to create a snapshot in order to download the current dashboard. Just use the Download icon and choose either PDF or CSV.

If you want to download a previously saved snapshot, open the snapshot, click the Download icon, and choose **Save as PDF**. Click **Exit Snapshot** in the upper right to return to the live dashboard.

#### Deleting a Dashboard Snapshot <a href="#deleting-a-dashboard-snapshot" id="deleting-a-dashboard-snapshot"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-90828d607fe4e98ce191161e93ee2fa3cdef6912%2Fdashboard-snapshot-delete.png?alt=media)

To delete an existing snapshot:

1.  1\.

    Go to any dashboard and click the camera icon in the upper right of the screen.
2.  2\.

    Choose **View All Snapshots**.
3.  3\.

    Choose the snapshot to delete to open it. Use the filter field to enter search text if needed.
4.  4\.

    With the snapshot open, click the gear icon in the upper right of the snapshot.
5.  5\.

    Click **Delete This Snapshot**.

Any customized dashboard can be shared with other account groups within the same organization by configuring the dashboard visibility. The built-in dashboard is shared only with the current account group.

There are separate permissions for sharing dashboards, and for snapshots as well: viewing other people's, viewing your own, and for creating snapshots that are externally viewable.

The differences between sharing a dashboard and sharing a snapshot link are:

*   Dashboard sharing is really a visibility setting for people already in your organization. They can view the live Dashboard anytime, by default seeing the most recent data. To share a live dashboard outside your organization, see

    [Embedding Dashboard Widgets in External Web Sites](broken-reference)

    ​
* Snapshot share links are for people outside of your organization or enterprise, and capture a point-in-time slice of data. To enable ThousandEyes customers to efficiently share events with third parties, “Snapshots” are unencrypted and may be accessed by anyone with the URL link. If you wish to limit access to test data, deselect **Link Sharing.**
* Snapshots can also be used internally to create a history, as otherwise ThousandEyes has limits on the historical data that is preserved.

Follow these steps to make your dashboard visible to other people within your organization, by account group.

1.  1\.

    Load the Dashboard you would like to share.
2.  2\.

    Click on the ellipsis

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-56e88a10b9f596d6397032af0c5b86cd08e187fb%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-7.png?alt=media)

    at the top right of the page and choose Edit Dashboard.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-00e7f25dea257f859f11fd1f72e78d88ff8c43e9%2Fdashboard-sharing-edit.png?alt=media)

1.  1\.

    Un-check **Set as Private** under Account Group Visibility.
2.  2\.

    Select Account Group Visibility as follows:

* Only current account group

1.  1\.

    If you select Specific account groups, use the second drop-down to select the account groups:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9c86aa032428f104a377b66a819fe2b39c264fd7%2Fdashboard-sharing-view-settings.png?alt=media)

#### Tracking Who’s Shared What <a href="#tracking-whos-shared-what" id="tracking-whos-shared-what"></a>

Under the Dashboard list, you can locate which dashboards were shared by you, or by other accounts:

*   Dashboard shared by you with other accounts are tagged as “Shared”

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dcc46638163ad4f1262cd4eac33d8f538277b4c9%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-10.png?alt=media)
*   Dashboard shared by other accounts with you are tagged as “Shared with me”

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8662a6fb9dd3583e0ac4bf08f1eb12c6f1a53ed5%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-11.png?alt=media)

### Sharing Dashboard Snapshots <a href="#sharing-dashboard-snapshots" id="sharing-dashboard-snapshots"></a>

You can share snapshots of dashboards manually via a publicly accessible URL, similar to snapshot sharing of test data. To share a snapshot of a dashboard, navigate to the desired dashboard and click the gear icon on the right-hand side to open the dashboard snapshot's additional options menu.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-414306fbf9b223cae9be0026a27e2221161fb497%2Fproduct-documentation\_reports\_working-with-reports-32.png?alt=media)

Here, click the **Link Share** toggle switch and the public URL for viewing this dashboard snapshot will be presented. You may copy the link to your clipboard and paste it into a document, an email, a chat or any other medium.

You may stop sharing the dashboard snapshot at any time by unchecking the **Link Share** switch shown above.

#### Emailing Dashboard Snapshots <a href="#emailing-dashboard-snapshots" id="emailing-dashboard-snapshots"></a>

You can select from a list of email addresses when setting up a scheduled snapshot. The options are for people inside your organization. You can’t enter a freeform email address.

If the intended viewers are outside of your organization, for example a third-party ISP or SaaS provider, you won’t be able to include third parties via scheduling automation.

To email the contents of a snapshot that was previously saved, open the snapshot and use the Download icon to save the snapshot as a PDF file that can be emailed manually as an attachment.
