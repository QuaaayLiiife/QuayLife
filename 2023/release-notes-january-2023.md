# Release Notes: January 2023

#### Updated Cloud Agent Names and Locations <a href="#updated-cloud-agent-names-and-locations" id="updated-cloud-agent-names-and-locations"></a>

We have updated several cloud agent locations and names for Azure, GCP, and AWS to match what they publish in their documentation. The changes are as follows, with the left hand side being the original name and the right hand side being the new name:

* Ashburn, VA (AWS us-east-1) -> N. Virginia (AWS us-east-1)
* Ashburn, VA - Oracle only (AWS us-east-1) -> N. Virginia Oracle only (AWS us-east-1)
* Ashburn, VA 2 - Oracle only (AWS us-east-1) -> N. Virginia 2 Oracle only (AWS us-east-1)
* Columbus, OH (AWS us-east-2) -> Ohio (AWS us-east-2)
* Dubai, UAE (AWS me-central-1) -> United Arab Emirates (AWS me-central-1)
* Dublin, Ireland (AWS eu-west-1) -> Ireland (AWS eu-west-1)
* Manama, Bahrain (AWS me-south-1) -> Bahrain (AWS me-south-1)
* Montreal, Canada (AWS ca-central-1) -> Central Canada (AWS ca-central-1)
* San Jose, CA (AWS us-west-1) -> N. California (AWS us-west-1)
* The Dalles, OR (AWS us-west-2) -> Oregon (AWS us-west-2)
* Amsterdam, Netherlands (Azure westeurope) -> Netherlands (Azure westeurope)
* Boydton, VA (Azure eastus2) -> Virginia (Azure eastus2)
* Cheyenne, WY (Azure westcentralus) -> Wyoming (Azure westcentralus)
* Chicago, IL (Azure northcentralus) -> Illinois (Azure northcentralus) (3 VAs affected)
* Chicago, IL - Oracle only (Azure northcentralus) -> Illinois Oracle only (Azure northcentralus)
* Chicago, IL 2 - Oracle only (Azure northcentralus) -> Illinois 2 Oracle only (Azure northcentralus)
* Des Moines, IA (Azure centralus) -> Iowa (Azure centralus)
* Dublin, Ireland (Azure northeurope) -> Ireland (Azure northeurope)
* Melbourne, Australia (Azure australiasoutheast) -> Victoria, Australia (Azure australiasoutheast)
* Phoenix, AZ (Azure westus3) -> Arizona (Azure westus3)
* Quincy, WA (Azure westus2) -> Washington (Azure westus2)
* Richmond, VA (Azure eastus) -> Virginia (Azure eastus)
* San Antonio, TX (Azure southcentralus) -> Texas (Azure southcentralus)
* Santa Clara, CA (Azure westus) -> California (Azure westus)
* Sydney, Australia (Azure australiaeast) -> New South Wales, Australia (Azure australiaeast)
* Midlothian, TX (GCP us-south1) -> Dallas, TX (GCP us-south1)
* New Albany, OH (GCP us-east5) -> Columbus, OH (GCP us-east5)

New Cloud Agents have been added to the following locations:

* Ashburn, VA, USA (Charter) (IPv6)
* Chicago, IL, USA (Comcast) (IPv6)
* Dallas, TX, USA (AT\&T) (IPv6)
* Dallas, TX, USA (CenturyLink) (IPv6)
* Dallas, TX, USA (Comcast) (IPv6)
* Dallas, TX, USA (Cox) (IPv6)
* Doha, Qatar (Azure qatarcentral)
* Kuala Lumpur, Malaysia (TIME)
* Kuala Lumpur, Malaysia (TIME) (IPv6)
* Los Angeles, CA, USA (AT\&T) (IPv6)
* New York, NY, USA (CenturyLink) (IPv6)
* San Jose, CA, USA (Comcast) (IPv6)
* Seattle, WA, USA (Charter) (IPv6)
* Seattle, WA, USA (Comcast) (IPv6)
* We have updated how page speed and response times are calculated for Endpoint Agent browser session tests when a page gets no response. Previously, the values shown in the page speed were not accurate, and the wait time was shown as "Response Time". This was misleading, as the browser never accessed the page. These values have now been updated to show a dash on non-responsive pages.
* The alert grid widget has now been removed from the platform and from snapshots. Customers can no longer create or view any alert grid widget in the platform.
* An issue that was preventing some BGP alerts from clearing even after the alert rule was modified and conditions were no longer met has been resolved.
* An issue that was incorrectly showing all Enterprise and Endpoint Agents as "online" in our map widget, even if some agents were offline at the time, has been resolved.
* An issue that was preventing users from duplicating existing custom webhook integrations has been resolved.
* An issue that was preventing some scheduled snapshots from being created for a short period of time has been resolved.
* An issue that was preventing a small handful of Endpoint alerts from clearing, even after all alert rules were removed from a test, has been resolved.
* An issue that was preventing users from using the **Alert Rules** filter on select dashboard widgets has been resolved.
* An issue that was incorrectly stating that some AppDynamics alert integrations were "Untested" even after they had been successfully tested has been resolved..

#### End of Installation Support for Ubuntu 18.04 LTS (“Bionic”) <a href="#end-of-installation-support-for-ubuntu-18.04-lts-bionic" id="end-of-installation-support-for-ubuntu-18.04-lts-bionic"></a>

Installation support for Ubuntu 18.04 LTS ("Bionic") will end on January 31st, 2023. This affects packaged agent installs, as well as image-based installations for the ThousandEyes virtual appliance, Intel NUC, and Raspberry Pi. Packages for Ubuntu 20.04 LTS ("Focal") are already available. Updated 20.04 LTS-based images for the ThousandEyes virtual appliance, Intel NUC, and Raspberry Pi are coming prior to January 31st, 2023.

As noted in our

[Ubuntu Linux Support Lifecycle](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/enterprise-agent-system-requirements/enterprise-agent-support-lifecycle#ubuntu-linux)

documentation, Ubuntu 18.04 LTS ("Bionic") will enter the End of Support period on April 30th, 2023 and End of Life on June 30th, 2023. Aligned to this, we will be ceasing support for the Cisco KVM deployment images for Cisco routers running IOS-XE 16.x. We recommend that customers migrate to deploying Docker-based agents for the Cisco Application Framework. For installation instructions, see

[Installing Enterprise Agents on Cisco Routers with vManage](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/cisco-devices/installing-enterprise-agents-on-cisco-routers-with-vmanage)

.

To assist customers with upgrading their agents to Ubuntu 20.04 LTS, we will be shipping upgrade scripts with the web-based UI on ThousandEyes Virtual Appliances, Intel NUC, and Raspberry Pi. This provides a pathway for in-place upgrades. For customers who wish to upgrade using the agent clustering method, you may do so as soon as the 20.04 images become available. For more information, see

[Replacing an Enterprise Agent Using the Agent Clustering Method](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/managing/replacing-an-enterprise-agent-using-the-agent-clustering-method)

.

#### ThousandEyes SAML Certificate Renewal <a href="#thousandeyes-saml-certificate-renewal" id="thousandeyes-saml-certificate-renewal"></a>

We have renewed the ThousandEyes SAML certificate and

[app.thousandeyes.com/saml-metadata](https://app.thousandeyes.com/saml-metadata)

now returns a new certificate. If you use a dynamic configuration for your SSO, your IdP server will automatically receive the new certificate. If you use a static or metadata-file configuration, you will need to update to the new certificate. For instructions, see

[ThousandEyes SAML Configuration](https://docs.thousandeyes.com/product-documentation/user-management/sso/how-to-configure-single-sign-on-with-metadata#identity-provider-side-configuration)

.

This update must be completed by February 18, 2023.

If your organization continues to use the old certificate for encrypting SAML assertion, users in your organization will no longer be able to log into ThousandEyes after February 18, 2023. The single logout feature will also be impacted.

#### Zoom Rooms Added to Zoom AST <a href="#zoom-rooms-added-to-zoom-ast" id="zoom-rooms-added-to-zoom-ast"></a>

In December 2022, an adjustment was made to include Zoom Rooms in the Zoom AST. For Zoom Rooms applications running on macOS and Windows, the Endpoint Agent client will activate for AST tests. This is enabled in Endpoint Agents running 1.141 version or later. Currently, this feature is in preview status while we verify the feature with beta customers.

#### Delete Agents with the Endpoint API <a href="#delete-agents-with-the-endpoint-api" id="delete-agents-with-the-endpoint-api"></a>

The Endpoint API has been extended to allow users to delete agents directly from the API. This extension provides users full control on the management of the agent via the API, by allowing customers to enable, disable, and delete any agent. For more information, see the

[API Documentation](https://developer.thousandeyes.com/v6/endpoint\_agents/#/endpoint\_agent\_delete)

.

* Users can now create Endpoint Agent labels that filter for agents that are not connected to a VPN, by using the "Not In" option of the **VPN Vendors** filter. This allows customers that are using one of the VPN vendors supported by ThousandEyes to identify agents that are not using that VPN, and apply a different set of tests to them.
* A new metric has been added to dashboards: **Page Load Completion**. This allows a user to understand if a page load was successfully completed and to calculate this percentage over time.

New Cloud Agents have been added to the following locations:

* New York, NY, USA (AT\&T) (IPv6)
* Rome, Italy (Telecom Italia)
* Rome, Italy (Telecom Italia) (IPv6)
* Rome, Italy (WINDTRE) (IPv6)
*   As previously announced on

    [December 21st, 2022](https://docs.thousandeyes.com/archived-release-notes/2022/2022-12-release-notes#2022-12-21)

    , the v7 reports API has officially been removed.
* An issue that was causing inconsistent transaction marker results between the test view and dashboard has been resolved.
* An issue with the filter selection on Internet Insights dashboard widgets that was preventing users from saving inputted domains as part of the filter has been resolved.
* An issue was found that impacted the line chart dashboard widget as users went from a specific scale selection to an auto scaled selection. As users navigated between the two options, the Y Axis would disappear. This has been corrected.

We are excited to announce the release of our first wave of Cloud Agent locations for Webex Calling. These Cloud Agents are installed inside the Webex Calling data centers around the globe, and will help you better monitor the performance of your Webex Calling environment. The following locations are now live:

* Chicago, IL, USA (Webex Calling)
* Dallas, TX, USA (Webex Calling)
* Frankfurt, Germany (Webex Calling)
* London, England (Webex Calling)
* Melbourne, Australia (Webex Calling)
* Osaka, Japan (Webex Calling)
* Sydney, Australia (Webex Calling)
* Tokyo, Japan (Webex Calling)
* Toronto, Canada (Webex Calling)
* Vancouver, Canada (Webex Calling)

Recorder IDE v1.6.0 has now been released. This release includes:

*   **Standalone Mode**: Permissions for the ThousandEyes Recorder IDE have been expanded. Users can now generate scripts with the Recorder IDE without permission to create transaction tests or use the credentials repository. Only **API Access** and **Login** permissions are required. For more information, see

    [ThousandEyes Recorder Permissions](https://docs.thousandeyes.com/product-documentation/browser-synthetics/transaction-tests/getting-started/thousandeyes-recorder-permissions)

    .
* **Test Settings** and the option to **Export to ThousandEyes** now include the following fields: **Exclude Domains/Object URLs**, **Screenshots**, **Camera and Microphone**, **Geolocation**, **Page Loading Strategy**, **Preferred Language**.
