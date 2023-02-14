# Network Outages

Network outage events represent a series of events that affect a large number of terminal interfaces and associated Network metrics at one or more points of presence of a given service provider (ASN).

### Network Outages View Timeline <a href="#network-outages-view-timeline" id="network-outages-view-timeline"></a>

On the **Internet Insights > Views** screen, the top portion shows a timeline, as shown in the image below. (Network Outages displays by default.)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-098d7f26b6aaafa747d37f60a4e03e359f4ba03b%2Finternet-insights-002-timeline-network-outages.png?alt=media)

### Network Outages Timeline Filters <a href="#network-outages-timeline-filters" id="network-outages-timeline-filters"></a>

The **Network Outages** timeline at the top of the view screen lets you filter or display data as follows:

* **Metric**: Affected Tests, Interfaces, Locations, or Outages
* **Outage Scope** is All or With Affected Tests, meaning you can limit application outages to only show those affecting your own tests.
* The **Network** filter lets you search for and choose one or more networks by name or Autonomous System (AS) number, for example IP-Max Network Services (AS 25091).

Click **Add a filter** to add filters including:

*
  * **Outage Scope** - same filter that’s already displayed
  * **Affected Provider** - choose by provider type (e.g., CDN), region, or by name
*
  * **Network** - same filter that’s already displayed
  * **Interface Location** - choose by region, country, or city
  * **Interface IP Address** - use the search box to narrow down the long list of numeric IP addresses
*
  *   **Affected Test** - these are tests potentially impacted by the outage, as described in

      [My Affected Tests](https://docs.thousandeyes.com/product-documentation/internet-insights/using-alerts-and-dashboards-with-internet-insights/my-affected-tests)

      ​
  * **Affected Hostname/Domain** - quickly search for a domain like “google.com” or a hostname like “myserver.domain.com”
  * **Server Location** - search by region, country, or city
  * **Server Prefix** - use to find a server with a particular IP prefix
  * **Server Network** - use to find by Autonomous System (AS) number or name, for example InterVoice, Inc. (AS 393222)

When you've selected a timeslice in the timeline, the **Internet Insights > Views > Map** tab shows a map of the outage(s) along with summarized outage information.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b796c9750b385556e7e68f07f835c602694a4d7b%2Finternet-insights-002a-network-outages-map-tab.png?alt=media)

### Network Outages Topology Tab <a href="#network-outages-topology-tab" id="network-outages-topology-tab"></a>

The **Internet Insights > Views > Topology** tab displays different information, depending on whether you have **Network Outages** or **Application Outages** selected as the view at the top of the screen.

If you have the **Network Outages** view selected, you’ll see a path visualization similar to the one shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0db8665aa095069f22d15af2a40366abd3a4e13b%2Finternet-insights-003-topology-network-view.png?alt=media)

On the Internet Insights **Network Outages** view topology, the nodes represent networks or locations, with sources on the left and targets on the right. See the

[Legend](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/path-visualization/using-the-path-visualization-view#legend)

on

[Using the Path Visualization View](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/path-visualization/using-the-path-visualization-view)

for a list of network node colors and their meanings.

* By default, sources are displayed as aggregated by country. IP and domain are not displayed. The number of agents is tabulated in the menu that appears when you hover over the source node.
* By default, intermediate nodes are aggregated by Autonomous System Number (ASN).
  * The menu that appears when you hover over the node shows the number of affected destinations and provides a link that shows the list of affected tests in a pop-up window.
  * Affected ASes are determined from public rDNS on the target IP and not target domain.
* By default, only links with 0% of traces and affected servers 10% are shown.
* Targets show the ASN and the number of affected interfaces in the view. The menu that appears when you hover over the node will show the number of affected destinations and provide a link that will show the list of affected tests in a pop-up window. Another link is available that shows only outages affecting the destinations relevant to that node.
* Click **Next nodes** (if available) to see more nodes impacted by an outage event.

Click on a node to show a focused path visualization for just that node, and use the **< Undo** button to restore the full path visualization.

#### Network Outages Topology and Grouping Filters <a href="#network-outages-topology-and-grouping-filters" id="network-outages-topology-and-grouping-filters"></a>

The **Topology** tab includes **Showing** (i.e., filtering) and **Grouping** options to highlight aspects of the topology visualization, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bd1215b0ec0815a83e8d58da49c100a01dbc3c18%2Finternet-insights-004-filters-topology-network.png?alt=media)

Nodes with outages are tallied under **Highlighting**. You can narrow the highlighting using the field **Highlight nodes that match all / any** and then choosing a list item such as Test name, Location, IP address, Prefix, or Domain. For example, if you choose Domain, a list of affected domains appears, and you can select one of those to highlight only those affected nodes on the path visualization.

**Showing** lists any currently applied filters. Click **Add a filter** to add multiple filters with these options:

* **Agents** filters - These are ThousandEyes cloud or your own ThousandEyes enterprise agents.
*
  * **Application** shows applications currently impacted by the outage selected in the timeline above
  *   **Affected Test** these are tests potentially impacted by the outage, as described in

      [My Affected Tests](https://docs.thousandeyes.com/product-documentation/internet-insights/using-alerts-and-dashboards-with-internet-insights/my-affected-tests)

      ​
  * **Hostname/Domain** - quickly search for a domain like “google.com” or a hostname like “myserver.domain.com”
  * **Server Prefix** - use to find a server with a particular IP prefix
  * **Server Network** - find by Autonomous System (AS) number or name
  * **Server Location** - search by region, country, or city
  * **Outage** - search by outage event
*
  * **Agents by**: Country, Origin, Location, Agent
  * **Destinations by**: Application, Server Network, Server Location, Server Prefix, Domain
* The red vs. blue in the sankey diagram corresponds to the Highlighting: Affected Agents field (a percentage slider).

### Network Outages Table Tab <a href="#network-outages-table-tab" id="network-outages-table-tab"></a>

When you've selected a timeslice in the timeline, the **Internet Insights > Views > Table** tab shows information about the outage(s) in table form. Click a network name to open details about the outage.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bcf352209f622ede213bbb889c1fcac02ff12f32%2Finternet-insights-002b-network-outages-table-tab.png?alt=media)
