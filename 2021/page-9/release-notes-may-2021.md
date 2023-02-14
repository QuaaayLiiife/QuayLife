# Release Notes: May 2021

#### New Protocol Options for Scheduled Tests <a href="#new-protocol-options-for-scheduled-tests" id="new-protocol-options-for-scheduled-tests"></a>

We have added a "Prefer TCP" option to Endpoint Agent scheduled tests that will ensure the test will fall back to ICMP + TCP Connect if no driver is detected, so that tests are still performed. This option is to avoid situations where Endpoint Agents are not included in TCP tests due to either the Windows driver missing, or agents running versions earlier than 1.75.0.

In addition, the **TCP Connect** checkbox has been removed, and replaced by additional **Protocol** options:

* Prefer TCP (fallback to ICMP)

#### New Onboarding for Catalyst Switching Customers <a href="#new-onboarding-for-catalyst-switching-customers" id="new-onboarding-for-catalyst-switching-customers"></a>

Starting this release, all Catalyst switching customers entitled to ThousandEyes will see a new onboarding workflow when visiting their newly created ThousandEyes organization. The workflow will guide them through creating agents, tests, and surface common use cases.

* The alert rules write API now supports the following alert rule metrics: certificate validity, TLS version, and weak cipher metrics.
* An issue was found where some users were receiving emails on cleared alert events even when they deselected the option to receive cleared alert emails in the UI. This has been resolved.
* An issue was found where gaps in data were incorrectly displayed on the timeline. This has been resolved.
* An issue was found in the v6 reports API where incorrect results were returned for certain 'groupValues' and 'groupProperty'. This has been corrected.
* An issue was fixed where changes to a filter on a report or dashboard widget weren't persisting, and reverted back to the previous filter. This has been corrected.
* API requests to **/v6/endpoint-tests/http-server/new** with the **groupId** missing now return a 400 rather than a 500 error. This is more explanatory, since the error is with the input rather than the server.
* An issue was found when an Endpoint Agent was uninstalled and later re-installed, where the **Last Contact** field would not accurately reflect the new Endpoint Agent installation date/last contact time. This has been corrected.
* An issue was found where newly created organizations were not able to use the AppDynamics Dash Studio integration due to a 0 API rate limit. This has been corrected and fixed for all customers.

#### Crypto Node.js Module in Transaction Tests <a href="#crypto-node.js-module-in-transaction-tests" id="crypto-node.js-module-in-transaction-tests"></a>

As of browserbot version 1.163.0 and ThousandEyes Recorder IDE version 1.1.0, the transaction test scripting sandbox now supports importing functionality from

[the Node.js crypto module](https://nodejs.org/api/crypto.html)

.

One way to leverage this new functionality is to compute an HMAC:

import { credentials } from 'thousandeyes';

import { createHmac } from 'crypto';

const dataToSign = 'hello, world!';

const hmac = createHmac('sha256', credentials.get('some-secret-key')).update(dataToSign).digest('base64');

* Previously, the VPN node in a path visualization merged with the first hop of the overlay. This caused some confusion with customers. We've updated the view so that the VPN node will stand alone in the path, and the first hop of the overlay will appear as a regular node.
* An issue was found where, for some disabled alerts, the alert would still fire if the conditions were met. This has been resolved.
* An issue was found where location alerts were failing to persist due to the metrics being reported as empty. This lead to location alerts not being cleared when they should have been, and has been resolved.
* An issue was found where the SSL certificate expiry alert rule was interpreted incorrectly, and caused an alert to fire when no certificates were expiring. This has been fixed.
* An issue was found where the API response to **/v6/tests/\<test id>.json** did not return all account IDs and their associated account group names if the user was associated with multiple organizations. This has been fixed.
* An Internet Insights issue was found where it appeared that some outages shown in the **Views** timeline were not being displayed in the **Overview** dashboard. This was because the **Overview** and **Views** timeline did not previously refresh at the same interval, resulting in windows where they would be briefly out of sync. The default refresh interval for the **Overview** has been lowered to match the **Views** timeline, and this resolves the issue.
* An issue was found where updating the test interval to a higher frequency (for example, changing from 5 minutes to 2 minutes) would cause the timeline to show gaps in data. This has been resolved.
* An issue was found where the alerting system was incorrectly interpreting the alert configuration, resulting in alerts firing when the conditions were not met. Alert configuration validation has been improved to resolve this issue.
* An issue was found where the **Availability** metric in reports and dashboards was showing as milliseconds instead of percentage. This has been fixed.
* An issue was found where, in some cases, the system was not properly appending agent details to alerts. This resulted in the UI incorrectly showing 0 triggered agents against an alert, and has been fixed.
* An issue was found where the global **Alert Start Time** for some alerts was showing as significantly before the **Alert Start Time** for the location alerts. This was caused by logic in the platform that carried the first instance of a condition violation for an agent, rather than the most recent violation. This logic has been updated, and the issue is now fixed.
* An issue was found where, if ICMP was blocked and preventing end-to-end metrics from being measured, a 100% packet loss alert would be triggered. This issue has been resolved.
* An issue was found where the number of agents shown to be running a scheduled test could differ between the **Timeline** and **Table** views. This occurred in instances where there were multiple data points for the same machine in the same round. The way the agent count is done has been adjusted, and only unique machines in a round will now be counted.
