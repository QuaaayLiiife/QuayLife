# Internet Insights

The Internet Insights module gives you macro-level visibility into outages that may affect you, using the collective intelligence of ThousandEyes’ entire agent network. The **Internet Insights > Overview** page presents a global map view of network outages and application outages, and a cross-layer visualization of those outages. This map shows the impact of worldwide internet events on individual users, and on enterprise networks at their edge devices.

ThousandEyes Internet Insights is powered by the collective intelligence of every test that’s run using the ThousandEyes platform. Customer data isn't exposed in this process; what's shared is that someone ran a test on a target using a ThousandEyes agent, and the target was unavailable. If enough agents testing towards the same target report problems, ThousandEyes makes the inference that the cluster of errors represents a real outage and displays it on the Outages map.

### Why Use Internet Insights? <a href="#why-use-internet-insights" id="why-use-internet-insights"></a>

"Is it just me, or am I affected by an internet outage?" is a common question to ask when a business-critical service is disrupted. Sometimes it’s not your own service, or the service you’re using, that is the problem. It could be an Internet provider or another node that’s impacting traffic, located elsewhere in the world. You can use Internet Insights to gain intelligence beyond what your own ThousandEyes tests can tell you.

Another common question is “Is it down?” meaning a SaaS platform, a cloud platform, or an Internet service provider. With self-reported outage dashboards, users can’t tell what is causing the problem or how widespread it is. Internet Insights shows more layers of information to evaluate probable causes. While end-to-end test data from individual tests can show where the communication failed for that particular test, Internet Insights can relate a single test error to broader failure patterns of geography as well as providers, domains, servers, and network interfaces.

Internet Insights outages display as _outage events_. Outage events can have a variety of causes, for example:

* Failures of physical infrastructure (for example, a major cable cut or loss of power at a facility such as an internet exchange)
* Failures of internet infrastructure due to political interference
* Distributed denial-of-service (DDoS) attacks

### How Are Outages Recognized? <a href="#how-are-outages-recognized" id="how-are-outages-recognized"></a>

The question here is what constitutes an outage that's important enough to appear as an outage event on Internet Insights, and how the data is used to determine when a cluster of server or test errors represents a genuine _outage event_. Internet Insights detects outage events by analyzing the network-layer and application-layer results of every test that is run from ThousandEyes Cloud Agents or Enterprise Agents. Internet Insights examines the path visualization data from each test, checking for path traces that terminate prior to their targets. Filters are then applied to the path traces and other Network-layer data to determine whether traces and the related test data represent a legitimate outage.

ThousandEyes' Internet Insights continuously monitors lossy interfaces across a wide range of networks and PoPs, maintaining a baseline for loss events. A Network Outage is triggered when a concentration of loss events is detected within a single network point of presence (PoP) within a short period of time.

Application Outages also requires data from multiple customers' tests. (This data is de-identified to protect customers' private information, as explained in

De-Identification of Data

.) This means that an outage is not reported based on an application that is used by only one customer.

For information on how Internet Insights defines an outage, see

[Outage](https://docs.thousandeyes.com/product-documentation/internet-insights/int-terminology#outage)

.

### How Internet Insights Displays Outages <a href="#how-internet-insights-displays-outages" id="how-internet-insights-displays-outages"></a>

The Internet Insights module features maps that show core internet infrastructure - including ISPs, DNS providers, IaaS, UCaaS, SECaaS, and CDNs - and prominent SaaS services such as Azure, Salesforce, and Twitter. It represents packets and links between routers geographically, showing current or past outages on a global map.

Internet Insights shows a macro view of outages - so you see what services are experiencing an outage and what other service providers are affected by it. It uses ThousandEyes agent data to isolate outage behavior to specific Autonomous Systems and locations, and to specific applications, then presents this information in a topological view.

You can also set up alerts based on Internet Insights data, to get notified about outages.

### Additional Internet Insights Notes <a href="#additional-internet-insights-notes" id="additional-internet-insights-notes"></a>

#### De-Identification of Data <a href="#de-identification-of-data" id="de-identification-of-data"></a>

How does ThousandEyes handle customers' test data to keep it anonymous in Internet Insights shared intelligence? ThousandEyes removes from the Internet Insights dataset any data that could identify customers (a process referred to as _de-identifying_) and aggregates the individual test data to ensure customer privacy. Data pertaining to private networks is filtered out of the dataset.

#### Internet Insights: Data-as-a-Service Offering <a href="#internet-insights-data-as-a-service-offering" id="internet-insights-data-as-a-service-offering"></a>

Internet Insights provides visibility into specific datasets derived from an aggregation of ThousandEyes tests running across the public internet (_packages_). ThousandEyes may elect to discontinue or modify Internet Insights packages at any time.

#### Public-Facing Outages Map <a href="#public-facing-outages-map" id="public-facing-outages-map"></a>

In addition to the Internet Insights visibility that is available through the ThousandEyes platform, ThousandEyes also maintains public-facing

[outages map](https://www.thousandeyes.com/outages/)

that displays a limited data set. Although the Outages Map does not have the same coverage as Internet Insights, the

[FAQ](https://www.thousandeyes.com/outages/faq)

section contains useful information that can aid in understanding the additional value that Internet Insights brings to your enterprise.
