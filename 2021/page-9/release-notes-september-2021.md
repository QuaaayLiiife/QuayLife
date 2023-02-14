# Release Notes: September 2021

#### Changes to Webapp Session Timeout Duration <a href="#changes-to-webapp-session-timeout-duration" id="changes-to-webapp-session-timeout-duration"></a>

In the coming weeks, ThousandEyes will change the default session timeout duration from indefinite to 30 minutes. This change will patch a security vulnerability, as well as better align the timeout duration with industry best practices.

As part of this change, the **keep\_session\_alive\_on\_auto-update** permission will be automatically removed from all default built-in roles. This change could affect customers that continuously display ThousandEyes dashboards (for example, in Network Operations Centers).

If you would like to preserve the **keep\_session\_alive\_on\_auto-update** permission for certain users within your organization, we recommend that you create a custom role with this permission and assign users in the appropriate account group to that role.

We will be temporarily disabling the **Billing History** view in the **Usage and Billing** section of the web app while we work on a fix to correct some inaccuracies we've noticed with the data presented there.

While we implement this fix, please reach out to your account representative for data on billing and usage for previous periods.

New Cloud Agents have been added to the following locations:

* Adelaide, Australia (IPv6)
* Chennai, India (JIO) (IPv6)
* Denver, CO, USA (Cogent) (IPv6)
* Falkenberg, Sweden (IPv6)
* Frankfurt, Germany (IPv6)
* Manila, Philippines (IPv6)
* Philadelphia, PA, USA (IPv6)
* Wellington, New Zealand (IPv6)

In addition, we've added AWS, Azure, and Google Cloud Platform Cloud Agents in the locations listed below. For a full list of Cloud Agents, see

[ThousandEyes Cloud Agent Locations](https://www.thousandeyes.com/product/cloud-agents)

.

**New Amazon Web Server Cloud Agents**

* Hong Kong (AWS ap-east-1)
* Manama, Bahrain (AWS me-south-1)
* Milan, Italy (AWS eu-south-1)
* Osaka, Japan (AWS ap-northeast-3)
* Stockholm, Sweden (AWS eu-north-1)

**New Azure Data Center Cloud Agents**

* Berlin, Germany (Azure germanywestcentral)
* Canberra, Australia (Azure australiacentral)
* Cheyenne, Wyoming (Azure westcentralus)
* Dubai, UAE (Azure uaenorth)
* London, England (Azure uksouth)
* Oslo, Norway (Azure norwayeast)
* Zurich, Switzerland (Azure switzerlandnorth)

**New Google Cloud Platform Cloud Agents**

* Delhi, India (GCP asia-south2)
* Hong Kong (GCP asia-east2)
* Jakarta, Indonesia (GCP asia-southeast2)
* Las Vegas, NV (GCP us-west4)
* Melbourne, Australia (GCP australia-southeast2)
* Osaka, Japan (GCP asia-northeast2)
* Salt Lake City, UT (GCP us-west3)
* Seoul, South Korea (GCP asia-northeast3)
* Toronto, Canada (GCP northamerica-northeast2)
* Warsaw, Poland (GCP europe-central2)
* Zurich, Switzerland (GCP europe-west6)

#### Updated Dashboards and Reports Caching Mechanism <a href="#updated-dashboards-and-reports-caching-mechanism" id="updated-dashboards-and-reports-caching-mechanism"></a>

The caching mechanism for dashboards and reports has been updated to improve end-to-end performance. As part of this change, the cache time has been increased from 5 minutes to 10 minutes. This will result in a delay in updated dashboards and reports when you change the ownership of a test to a different account or organization ID.

For example, if the test ownership moves from Account Group A to Account Group B, this change will only be reflected in a customer's dashboard or report when the cache is updated, meaning there is a maximum potential delay of 10 minutes.

* Previously, searching the Endpoint Agent **Agent Settings** filter list for values of any of four specific metrics (User, VPN Gateway Address, VPN Client Address, or VPN Client Network) would not work correctly. This has been resolved.
* A display issue caused new Endpoint Agents to only display the username, but not the agent name for the host device. Both agent name and the username are now displayed again on the Agent Settings page.
* Previously, some alerts were not clearing, even after the associated alert rule was disabled or deleted. This was due to a configuration propagation issue that has since been corrected.
* An issue was fixed where report and dashboard widgets were incorrectly inheriting names of previously named widgets on save.

#### Changes to the te-browserbot Package's Dependencies on RHEL 7 and Oracle Linux 7 <a href="#changes-to-the-te-browserbot-packages-dependencies-on-rhel-7-and-oracle-linux-7" id="changes-to-the-te-browserbot-packages-dependencies-on-rhel-7-and-oracle-linux-7"></a>

In the coming months, as part of an architectural change to BrowserBot, ThousandEyes will add

[**te-podman**](https://podman.io/)

as a dependency of the **te-browserbot** package. This new package depends on some packages available in the Red Hat Enterprise Linux 7 Server - Extras and Oracle Linux Addons repositories for RHEL 7 and Oracle Linux 7, respectively.

Users with existing agents running on RHEL 7 should enable the **rhel-7-server-extras-rpms** repository. Users with existing agents running on Oracle Linux 7 should enable the **ol7\_addons** repository. Otherwise, BrowserBot will not be able to upgrade to this forthcoming version.

On RHEL 7, you can enable this required repository by executing `subscription-manager repos --enable=rhel-7-server-extras-rpms`. On Oracle Linux 7, execute `yum-config-manager -q -y --enable ol7_addons`.

New Cloud Agents have been added to the following locations:

* Mumbai, India (JIO) (IPv6)
* An issue was found in the Stacked Area graph widget for reports and dashboards when displaying a **Page Load** metric. The calculation for the metric was adding DOM load time to the page load time, which is incorrect, as DOM load time is a sub-component of page load time. This has now been resolved and the correct value is displayed.

#### Metric Calculation Improvements for Reports and Dashboards <a href="#metric-calculation-improvements-for-reports-and-dashboards" id="metric-calculation-improvements-for-reports-and-dashboards"></a>

We have improved the way we calculate the **Availability** metric for Device data in reports and dashboards. Availability is now calculated based on the number of interfaces that are up and running divided by the number of interfaces that the admin set as up. This is a slight change to the previous calculation, which also included in rare instances interfaces that were up and running even if they were set as down by the admin.

Additionally, customers can now query **Device Availability** by median, max, min, Nth percentile and standard deviation.

#### Changes to Update Email Limit <a href="#changes-to-update-email-limit" id="changes-to-update-email-limit"></a>

Effective immediately, ThousandEyes will be making an update to our profile logic so that requests to update the email address of a provisioned user will only be accepted a maximum of once per hour. Once that limit is reached, subsequent requests to update email will then be blocked by the system until the hour period has passed. This change will patch a security vulnerability. We do not anticipate this change to affect customer account access outside of the above limitation.

#### Endpoint Agent Notifications Update <a href="#endpoint-agent-notifications-update" id="endpoint-agent-notifications-update"></a>

We have moved Endpoint Agent notifications to our new backend notifier. This results in several changes to notifications, including:

* Added **ruleName**, **violationCount**, **ruleAID**, and **type** as new fields.
* Changed **browserSessionAlert** to **alert**.
* Added a permalink, but maintained the soon to be deprecated **link** field.
* Most strings are now in human readable format.

These changes should not require customers to update their webhooks. However, you should review your downstream systems to ensure there is no impact.

* Changed from **Browser Session (Application)** to **Browser Session Application**.
* The order of **Start Date** and **Number of Sites Visited** is flipped.
* Changed from **Scope** to **No. of Agents**.
* Added **No. of Visited Sites**.
* Changed from **AlertID** to **Alert ID**.
* Removed the dedicated field for **ruleExpression** and instead have the human readable form in the **Alert Rule** field.
* Removed the dedicated field for **ruleExpression** and instead have the human readable form in the **Alert Rule** field.
* Added **Target** and **Test Names** as fields.
* Changed from **Scope** to **No. of Agents**.

New Cloud Agents have been added to the following locations:

* Louisville, KY, USA (IPv6)
* New York, NY (Cogent) (IPv6)
* Previously, if an Endpoint Agent user was connected via a remote desktop, the temporary directory would change. This caused requests for the temporary directory location to fail, as system processes were still using the previously configured location. This has been resolved.
* Previously, an issue was found where grouping by devices in a report or dashboard widget was not correctly populating individual device names. This has been resolved.
