# Terminology

This section explains the terminology used in the Internet Insights module, and describes its basic concepts.

The term _application_ refers to a service, OSI application layer 7 of the OSI stack, as opposed to a network interface. Application outages are displayed by affected domain rather than by Autonomous System (AS) number. An example of an application outage would be an outage in **oracle.com**, whereas a network outage might affect Oracle HCM AS4192. Note that these two types of outages won’t necessarily occur at the same time.

An _application outage_ is an event for which some or all servers that belong to the same application are failing. More specifically, an application outage is an event that causes the number of affected servers of a given application to exceed the Internet Insights error thresholds. The thresholds include criteria such as number of ThousandEyes Cloud or Enterprise Agents that see the affected servers, and total number of servers seen per application.

Not all errors are classified as "application errors". This classification is done using curl code, HTTP code, and problem details. A server is defined as a tuple (hostname, ip address). Error information is extracted based on a mapping between URLs and applications. For example, the URL **www.amazon.com** is mapped to the Amazon application.

### ASN (Autonomous System Number) <a href="#asn-autonomous-system-number" id="asn-autonomous-system-number"></a>

An ASN is a unique number assigned to an organization (also referred to as _service provider_) that operates one or more networks. ASNs are used by the Border Gateway Protocol (BGP) to construct the Internet's routing tables. A list of ASNs, the names of their operators, and the network blocks included under the ASN can be found at . An example of a service provider and its associated ASN is ThousandEyes, which is assigned ASN 394101.

The Internet Insights _catalog_ is a database of service providers, categorized by provider name, provider type and either ASNs or networks (for providers who operate public networks not associated with their ASNs).

The types of service providers are:

* Content Delivery Networks (CDN)
* DDoS Mitigation providers, or Security-as-a-Service (SECAAS)
* Infrastructure-as-a-Service providers (IAAS)
* Internet Service Providers (ISP)
* Software-as-a-Service providers (SaaS)
* Unified communications as a service providers (UCaaS)

The geographic regions are

* Europe, Middle East and Africa (EMEA)

An _interface_ is a publicly-accessible IP address belonging to a node in a path trace. A single path trace can detect only one interface per node. An interface represents the point of interconnection between a computer and a private or public network, for example a router. Interfaces are part of a network’s infrastructure, related to a network outage and its scale.

For example, in the Path Visualization below, the **Show IP Address labels** setting has been selected to show each node’s discovered interface.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4978acacc77c2d78a9ae8bb0b8ca2bc263566552%2Fproduct-documentation\_internet-insights\_int-terminology-1.png?alt=media)

The Path Visualization shows a test run by four Cloud Agents, each generating three path traces (the default configuration for most test types). The three traces from each agent travel one path until the node with interface 4.69.133.109. The path traces then discover paths through the three nodes with interfaces 205.129.17.238, 4.35.37.174 and 4.35.35.38 (one path trace per node). The traces then converge and follow a common path, terminating at a node with IP address 64.79.159.26, prior to the target of the test, 204.115.101.231.

A _network_ is a block of continuous IP addresses, specified in Classless Inter-Domain Routing (CIDR) notation. An example of a network expressed as a CIDR block is 198.160.62.0/23, which is the network containing the two terminal interfaces from the previous image.

_Network outages_ in Internet Insights are events with 100% packet loss in the same Autonomous System (AS) and the same metropolitan location during the same period of time, with a certain level of impact on infrastructure, sensors and services. More specifically, an _outage_ is an event or series of events that causes the number of terminal interfaces and associated Network metrics at one or more points of presence of a given service provider (ASN) to exceed the Internet Insights thresholds. These system-defined thresholds include criteria such as the number of Cloud or Enterprise Agents running the affected tests, the number of test destinations affected, and end-to-end packet loss in those tests.

For example, in a given round of test data, say Internet Insights detects eight terminal interfaces in three networks that belong to one service provider/ASN. Those interfaces' IP addresses are located in two points of presence belonging to that service provider. If the associated data from all affected tests passes the filter criteria, Internet Insights indicates an outage in that service provider.

A _node_ is a device such as a router, load balancer or firewall that is discovered by one or more path traces from the Path Visualization view. Nodes possess at least two interfaces (typically more) and perform IP forwarding (that is, routing) between interfaces.

### Package and package license <a href="#package-and-package-license" id="package-and-package-license"></a>

A _package_ is a collection of Internet Insights providers with the same type and region. Customers license a package in order to display outages originating from the providers included in the package.

An example of a package is the provider type **ISP** in the region **North America**. This package contains providers in North America who are classified as Internet service providers. The example from

_Provider_

below with provider CenturyLink would be included in this package.

In addition, because CenturyLink has points of presence in other locations, this provider appears in two other packages of type **ISP**. The other packages have regions of **EMEA** and **Asia Pacific**.

A _PoP_ is the physical location of one or more interfaces belonging to a given service provider. Internet Insights specifies PoPs based on the provider’s ASN number and a geographic location.

Private data centers, colocation data centers, and Internet exchanges (IXs) are examples of PoPs.

An Internet Insights _provider_ is a unique combination of provider name, provider type, and geographic region, in addition to other data.

CenturyLink is also listed as a provider in three other regions. All will have the same provider type, but other data could vary.

For Internet Insights Application Outages, a _server_ represents an IP/hostname combination, for example salesforce.com on one IP address. A server represents a computing device that serves content for websites and web applications, and is part of an application’s infrastructure, sometimes segmented by geographical region.

A _terminal interface_ is an interface in a path trace where the trace ends before the target of the test. It is the last responding IP address of that path trace. No trace responses are received from subsequent intermediate nodes beyond the terminal interface's node, nor from the target itself.

For example, consider the path trace in Figure 2 below, from the Cloud Agent in Boston, Massachusetts, to the nodes outlined in red, with interfaces 198.160.62.181 and 198.160.62.183, respectively.

​

![Figure 2](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-18d4905d5487c63689ea082b9a6cd29ec40649a1%2Fproduct-documentation\_internet-insights\_int-terminology-2.png?alt=media)

**Figure 2**

No intermediate nodes beyond the red outlined nodes have responded to the Boston Cloud Agent. Additionally, the agent is solid red in color, indicating no response (100% end-to-end loss) from the target, 136.147.108.189. Therefore, 198.160.62.181 and 198.160.62.183 are classified as terminal interfaces.

Note that in Figure 1, the red-outlined node with interface 64.79.159.26 is not a terminal interface because the target responded to end-to-end metrics (the separate probes for loss, latency, and jitter) as indicated by the green color of the agents.
