# Application Outages

ThousandEyes’ Application Outages feature provides an app-centric view of the status of widely-used SaaS and other services (layer 7 of the OSI model, meaning the application layer). Rather than consulting a service's status page, which is typically updated manually and might not accurately state the beginning and end times of an incident, ThousandEyes’ Application Outages shows a real-time, data-based view of the outage. Because they’re based on real data, the visualizations in Application Outages provide credibility to effectively escalate issues with service providers.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-88a5e77a35e7f35ed4a5a3032246cf082013b753%2Finternet-insights-007-application-outage-map.png?alt=media)

The image above is filtered to show only Application Outages.

With the addition of the Application Outages feature, Internet Insights offers cross-layer visualization, in which you can see what type of outage is occurring - network or application. Application Outages also identifies the specific outage error type for each affected application. You can use this combined insight to reduce your organization's mean time to identify (MTTI).

### Application Outages View Timeline <a href="#application-outages-view-timeline" id="application-outages-view-timeline"></a>

To see the View screen for Application Outages, choose **Internet Insights > Views** and then click **Application Outages** next to the timeline. (Note that Application Outages don’t always perfectly coincide with Network Outages.)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2aa3d9965bf0037475d3bcbe4ef815271cdd579f%2Finternet-insights-008-application-outage-timeline.png?alt=media)

#### Application Outages Timeline Filters <a href="#application-outages-timeline-filters" id="application-outages-timeline-filters"></a>

The Application Outages timeline at the top of the view screen lets you filter or display data as follows:

* **Metric**: Affected Tests, Servers, Locations, or Outages
* **Outage Scope** is All or With Affected Tests, meaning you can limit application outages to only show those affecting your own tests.
* The **Application** filter lets you choose one or more application types, or applications by domain, with major categories for:
  * **Collaboration and Messaging**, for example Miro (miro.\*)
  * **Communication**, for example Microsoft Teams or Slack.
  * **E-Commerce**, for example Amazon or Walmart.
  * **Enterprise Productivity** includes services like Amazon, Dropbox, various Google apps, and Microsoft Office 365.
  * **Finance** includes online finance portals such as Citibank and PayPal.
  * **HR** includes human-resource management tools such as Workday and ADP payroll processing.
  * **Cloud** includes services such as Amazon Web Services, Azure, and Google Cloud.
  * **Developer Tools** includes services like Okta, Splunk, Atlassian.net and GitHub.
  * **Sales and Marketing** includes services such as Salesforce and MailChimp.
  * **Security** includes password services and Cisco Meraki.
  * **Social Media** includes popular social-media platforms such as Facebook, LinkedIn, and YouTube.

### Application Outages Topology Tab <a href="#application-outages-topology-tab" id="application-outages-topology-tab"></a>

The **Topology** tab for Application Outages shows traffic flow between agents and destinations. A typical default view is shown below, with ThousandEyes agents grouped by country (origin or location). If there are multiple outages in progress, there could be multiple destinations as well. As a basic guideline, keep in mind that healthy nodes are blue; problem nodes are red.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-377f9d2bb73e90c39bb389b7f93286eb6ea8b3c2%2Finternet-insights-009-application-outage-toplogy.png?alt=media)

Select an outage on the timeline above in order to see data on the **Topology**, **Map**, and **Table** tabs below.

#### Application Outages Topology and Grouping Filters <a href="#application-outages-topology-and-grouping-filters" id="application-outages-topology-and-grouping-filters"></a>

Filtering options for the Application Outages **Topology** tab allow you to set different levels of granularity and also thresholds for visual severity, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0db260a098c306e266796837520f0c6ba4786b43%2Finternet-insights-010-application-outage-topology-filters.png?alt=media)

**Showing** lists any currently applied filters. Click **Add a filter** to add multiple filters with these options:

* **Agent** filters - These are ThousandEyes cloud or your own ThousandEyes enterprise agents.
*
  * **Application** shows applications currently impacted by the outage selected in the timeline above
  *   **Affected Test** these are tests potentially impacted by the outage, as described in

      [My Affected Tests](https://docs.thousandeyes.com/product-documentation/internet-insights/using-alerts-and-dashboards-with-internet-insights/my-affected-tests)

      ​
  * **Hostname/Domain** - quickly search for a domain like “google.com” or a hostname like “myserver.domain.com”
  * **Server Prefix** - use to find a server with a particular IP prefix
  * **Server Network** - find by Autonomous System (AS) number or name
  * **Server Location** - search by region, country, or city
*
  * **Agents by**: Country, Location, Origin Network, or Agent
  * **Destinations by**: Application, Server Network, Server Location, Server Prefix, or Domain
* The red vs. blue in the sankey diagram corresponds to the Highlighting: **Affected Agents** field (a percentage slider).

#### Agent Groups and Server Groups <a href="#agent-groups-and-server-groups" id="agent-groups-and-server-groups"></a>

Hover over a link, a source, or a destination in the sankey diagram for Application Outages (**Internet Insights > Views**, **Topology** tab) to see affected servers, your affected tests, and affected agents, as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-24c5a0e6b97ba1e361cd54c8c3bc5558e1c7a870%2Finternet-insights-010x-application-outage-agent-groups.png?alt=media)

* **Source**. The source displays on the left. In this case, there are 3 agents in the United States reporting problems accessing applications including Microsoft Online, Microsoft Office365, Salesforce, and Google.
* **Link**. Hovering over a link narrows down the statistics to include both the source and a single destination. Within the link tooltip:
  * **Tests from Agent Group**. Percentage of affected tests from this source. Source is shown based on filtering and grouping criteria selected.
  * **Tests to Server Group**. Percentage of affected tests with the same destination. Destination is shown based on filtering and grouping criteria selected. In this case, the affected tests originating from the agents in the United States represent 33% of affected tests targeting Microsoft Online.
* **Destination**. The target destination displays on the right. It shows the number of affected servers, number of outages, and which of your tests are affected by this outage.

### Application Outages Map Tab <a href="#application-outages-map-tab" id="application-outages-map-tab"></a>

When you've selected a timeslice in the timeline, the **Internet Insights > Views > Map** tab shows a map of the outage(s) along with summarized outage information.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d463fcc546243b04e8d8bee340a1840b420d72f9%2Finternet-insights-010b-application-outage-map-tab.png?alt=media)

### Application Outages Table Tab <a href="#application-outages-table-tab" id="application-outages-table-tab"></a>

The **Table** tab for the Internet Insights Application Outages view includes information on the error type details, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c27dd7792203d3e493e899691ad625bcca94f534%2Finternet-insights-011-application-outage-table-tab.png?alt=media)

Click the **Error Type Detail** column for one of the **Table** tab entries to see what is contributing to this application outage. In the example below, an application outage for okta.com shows server and network timeouts affecting 42 servers and up to 53% of the ThousandEyes agents that are running tests that involve this domain.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a5c5f23b20f89ea54e50bcb00bb6256ddd1c64d9%2Finternet-insights-012-application-outage-topology-table-tab-error-type.png?alt=media)

### How Application Outages Works <a href="#how-application-outages-works" id="how-application-outages-works"></a>

Whereas the Network Outages feature shows collective intelligence about outages in _internet infrastructure_, Application Outages uses the same approach to show information about the availability of critical _applications_, such as Zoom, Salesforce, PayPal, and Twitter.

“Coverage” of applications is driven by what’s most important to current ThousandEyes customers, based on what tests they’re already running. Other guidance comes from SSO providers such as Okta, which lists the top business apps that their SSO customers are using.

In order for an application to be trackable in Internet Insights, a critical mass of data must exist first. If a single ThousandEyes customer test on a particular target fails, there’s not enough information to determine if this is truly a public-facing outage. However if tests of various types from different customers on the same target fail, or encounter similar errors midway through the routing process, the outage is likely to have greater impact.

#### Alert on Application Outages <a href="#alert-on-application-outages" id="alert-on-application-outages"></a>

If you have configured ThousandEyes tests against your own infrastructure, you can set up Internet Insights alerts so that you are notified when there is an outage that affects your tests.

Then, in the case of an outage, use the cross-layer visualization to find the source of the issue and guide how you resolve it.

#### Alerting on Application Outages using the API <a href="#alerting-on-application-outages-using-the-api" id="alerting-on-application-outages-using-the-api"></a>

You can use v7 of the ThousandEyes API to work with alerts based on data from the Application Outages feature. For details, see

[the developer documentation](https://developer.thousandeyes.com/v7/alerts/#/alert-details)

.

### Viewing Application Outages Elsewhere in the ThousandEyes Platform <a href="#viewing-application-outages-elsewhere-in-the-thousandeyes-platform" id="viewing-application-outages-elsewhere-in-the-thousandeyes-platform"></a>

Application Outages data is included in various parts of the ThousandEyes platform. The primary ones are listed below.

* For any widget that can draw on Internet Insights as a data source, you can set the **Category** field to either **Network Outages** or **Application Outages**. The widget will then display the metrics used in Application Outages.
* The **Internet Insights** tab lists alert rules that you have configured for outages. The table includes a **Type** column, where you can see whether the alert rule is for network outages or application outages.
* For any widget that can draw on Internet Insights as a data source, you can set the **Category** field to either **Network Outages** or **Application Outages**. The widget will then display the metrics used in Application Outages.
* In the list of saved events, the **Event Type** column shows whether the event is an **Internet Insights** event.
