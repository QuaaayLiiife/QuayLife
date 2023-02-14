# Global Vantage Points

ThousandEyes' global vantage points are lightweight, Linux-based software agents that allow users to run a variety of layered monitoring tests, in order to gain insight into network and application performance and user experience.

### Comparison of Agent Types <a href="#comparison-of-agent-types" id="comparison-of-agent-types"></a>

ThousandEyes provides three types of agent. Each type of vantage point provides similar capabilities, but serves different purposes, and exists in different environments:

Cloud Agents are installed and maintained by ThousandEyes, and are available immediately to customers to configure tests, with no administrative responsibilities. Cloud Agents are located in many cities and countries; see

[this map](https://www.thousandeyes.com/product/cloud-agents)

for the current list of locations. These agents provide "outside-in" visibility to web-based apps or API endpoints.

Cloud Agents provide most of the configuration options that Enterprise Agents provide, but because Cloud Agents are used by multiple customers, some features are not available. For example, Cloud Agents cannot be configured to run web-layer tests through a proxy server, as this would require all tests run by the agent to use the proxy. For use cases such as testing a cloud-based proxy server, customers must use Enterprise Agent or Endpoint Agent.

Enterprise Agents are deployed by customers within their own infrastructure.

An Enterprise Agent can run every ThousandEyes test type (except Network Layer BGP tests, which are not run by agents). Additionally, Enterprise Agents can be either a source or target of an agent-to-agent test, which provides bi-directional network data (end-to-end metrics and the Path Visualization view) between itself and another ThousandEyes agent (Cloud or Enterprise).

Enterprise Agents are intended to be installed in server-type environments, and be online continuously in order to run scheduled tests. Enterprise Agents require systems administrators to provide resources such as time synchronization and firewall/packet filter rules for test and administrative traffic.

An Enterprise Agent can be installed in a virtualized environment (virtual machine or container) as well as installed directly on native Linux systems, and on certain types of hardware, such as Intel NUC or Cisco ISR and ASR routers. Installing the Linux package on a supported Linux distribution with administrative (root) access will provide extensive flexibility. Customers can combine Enterprise Agent functionality with other capabilities of the host, such as advanced routing and proxying, PKI/certificate functionality or other authentication, authorization and access control (AAA) technologies.

Endpoint Agents are installed on a PC or Mac, and provide on-demand and real-time visibility into each employee’s experience of SaaS and internally-hosted apps, as well as underlying wireless LAN, WAN, Internet connectivity and system health.

For tests, Endpoint Agents have the most specialized purpose: to collect Web-layer “waterfall” data (i.e., HTTP archive format) and Network-layer data (including layer 2 information such as WiFi data) from workstation environments (although Windows Server installations are supported). Data collection is often performed on-demand, activated when a user experiences performance or other problems with web-based applications.

Endpoint Agents are quickly and easily deployed as browser plug-ins for Chrome or Internet Explorer, and can monitor any application that Chrome and Internet Explorer can access.
