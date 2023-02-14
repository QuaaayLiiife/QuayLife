# Release Notes: December 2022

#### Alert Grid Widget Deprecation <a href="#alert-grid-widget-deprecation" id="alert-grid-widget-deprecation"></a>

After December 20, 2022, you will not be able to add new alert grid widgets to dashboards. The widget type will be removed on January 20, 2023. Existing alert grid widgets will be removed from the platform and from snapshots. ThousandEyes recommends that you replace these alert grid widgets with alert list widgets if desired.

#### Endpoint Agent Browser Session support for Custom Webhooks <a href="#endpoint-agent-browser-session-support-for-custom-webhooks" id="endpoint-agent-browser-session-support-for-custom-webhooks"></a>

ThousandEyes custom webhooks now support Endpoint Agent browser session alert types. You can now create custom webhooks and attach them to any Endpoint Agent browser session alert rule.

* Browser session tests from the Endpoint Agent have updated how Page Speed and Response times are calculated for pages where we get no response. Before, not fully accurate values were shown in the Page Speed and the wait time was shown as "Response Time". This was misleading because the browser never accessed to the page. These values have been updated to show a dash instead in those cases.

New Cloud Agents have been added to the following locations:

* Ashburn, VA, USA (Comcast) (IPv6)
* Ashburn, VA, USA (Verizon) (IPv6)
* Ashburn, VA, USA (AT\&T) (IPv6)
* Chicago, IL, USA (CenturyLink) (IPv6)
* Chicago, IL, USA (Charter) (IPv6)
* Chicago, IL, USA (Verizon) (IPv6)
* Dallas, TX, USA (Comcast) (IPv6)
* New York, NY, USA (Comcast) (IPv6)
* San Jose, CA, USA (Charter) (IPv6)
* Endpoint Agent: An issue has been fixed in the **Wireless** tab of the **Local Network** tests in the **Views** section. When the user filters by **Agents**, the Endpoint Table is no longer incorrectly showing "No Data", and instead the results are now consistent with the BSSID Table.
* Endpoint Agent: The application of test configuration changes (e.g., changes of priority) in the Endpoint Agent has been improved and it will now take immediate action, or at last in the next check-in of the agent.
* Endpoint Agent: An issue that was showing an incorrect format for the retransmission rates in the Endpoint and BSSID tables of the **Local Network** tests has been resolved.
* Endpoint Agent: An issue has been fixed in the Automated Session Test (AST) widget of the Dashboard section. The filter by Target IP does now show the correct list of IPs available.
* Dashboard: Fixed an issue that was creating blank filters for some Dashboard widgets.
* Alerts: An issue that was preventing some customers in EU from assigning alert suppression windows to tests has been resolved.
* Account Management: An issue was allowing customers to create identical users in the same account. This has now been resolved, and an error is displayed, if an existing user gets created a second time.
* Revenue Platform: Fixed an issue in the usage consumption calculator that showed inaccurate unit consumption that did not match what customers saw when creating tests. This issue occurred specifically with agent-to-agent tests.
* Revenue Platform: An issue was causing a low response from the **/v6/tests/#/test\_update** API. This has now been resolved and the previous response times have been restored.
* BrowserBot: Fixed issues related to the exclude domains feature on page load and transaction tests.

#### IPv6-Only Virtual Appliance Support <a href="#ipv6-only-virtual-appliance-support" id="ipv6-only-virtual-appliance-support"></a>

We have updated the ThousandEyes console and web UI for the virtual appliance as part of an ongoing effort to improve IPv6 support within the agent. These improvements include:

* When configuring DNS manually in the web UI, there are now four configuration fields, and support for adding IPv6 nameserver addresses.
* When IPv6 is set to `Auto`, all relevant network information is now shown in both the console and web UI, the same as when it is set to `Manual`.
* The link-local IPv6 address is no longer shown on the network interface. Instead, only valid routable addresses will be shown if they are configured.
* It is now possible to disable IPv4 from the console directly when manually configuring networking, to support IPv6-only networks.

In addition, the following functionality has been removed:

* Two status checks in the diagnostics tool within the web UI have been removed. These are the reachability check for the ThousandEyes API and the validity check for the account group token. The reachability check is no longer needed, and the validity check has been made redundant as part of the process for submitting the token in the UI.

#### Default Windows Endpoint Installation Now Includes TCP Support <a href="#default-windows-endpoint-installation-now-includes-tcp-support" id="default-windows-endpoint-installation-now-includes-tcp-support"></a>

As more and more customers leverage our Automated Session Tests, most require the TCP network tests provided through the NPCAP library. Starting on 31 January, 2023, the MSI installation default will include TCP test support to ease installation. This consists of the NPCAP library. Endpoint Agents that have not previously been installed with the TCP tests option will not be impacted and continue with their original installation preference.

Starting on 31 January, 2023, when a new installer is downloaded, the NPCAP library, with the TCP test option, will be included by default. Customers may remove this option during installation with an MSI switch or by unselecting the option in the installer.

#### New Workflow for Registered User Email Change/Update <a href="#new-workflow-for-registered-user-email-change-update" id="new-workflow-for-registered-user-email-change-update"></a>

We are introducing a new workflow for updating or replacing a registered user's email address. Previously, a message was sent only to the new email address. With this change, if a user attempts to update their email address, a confirmation email message will be sent to both their old email address and the new email address. The email address will only be updated for a user if both email messages are confirmed.

#### Credential Entry Masking for Custom Webhooks <a href="#credential-entry-masking-for-custom-webhooks" id="credential-entry-masking-for-custom-webhooks"></a>

Custom webhook security has been improved, as we now automatically mask all credential entries in the UI.

#### New Internet Insights Catalog Entries for SaaS Providers <a href="#new-internet-insights-catalog-entries-for-saas-providers" id="new-internet-insights-catalog-entries-for-saas-providers"></a>

The Internet Insights catalog now includes coverage of the following SaaS providers:

* **Streaming:** HBO Max, Hulu, Netflix, Spotify (new category).
* **Finance:** Cash App, Venmo.
* **Collaboration & Messaging:** WhatsApp.
* **Social Media & Networking:** TikTok.

New Cloud Agents have been added to the following locations:

* Anchorage, AK, USA (IPv6)
* Los Angeles, CA, USA (Comcast) (IPv6)
* Pittsburgh, PA, USA (Comcast)
* Pittsburgh, PA, USA (Comcast) (IPv6)
* To further improve the usability of the new browser options settings for page load and transaction tests, new button selection and more hover over text has been added.
* The v7 API Integrations endpoints now use a string UUID for the `integrations id` field instead of a numeric ID.
* An issue that caused the virtual appliance web UI to not show the correct DNS hostname provided by the DHCP server has been resolved.
* An issue that caused the virtual appliance interfaces that were configured as “auto” / “dhcp” and assigned with no valid address to show up as 'configured' has been resolved, and they will now show as an empty value.
* An issue that was preventing BGP alerts from clearing after the alert rule was updated or removed from a test has been resolved.

#### v7 Reports API Deprecation <a href="#v7-reports-api-deprecation" id="v7-reports-api-deprecation"></a>

With the merging of reports functionality into ThousandEyes dashboards, the v7 Reports API is now deprecated and will be removed in January, 2023.

If your organization used v7 Reports API endpoints in the past, we recommend you now use the

[v7 Dashboards API](https://developer.thousandeyes.com/v7/dashboards/)

. You should expect slightly different responses from the v7 Dashboards API, but full feature parity.
