# Working with Enterprise Agent Clusters

In environments where there are more than one enterprise agent running in a single location, administrators may want to simplify the agent selection process for their end users, by abstracting the number of Enterprise Agents running from a single location into an agent cluster. Additionally, clustering provides the benefit of assigning new tests to the least utilized member of a cluster, for the given test type.

ThousandEyes Cloud Agents operate using the same concept as Enterprise Agent clusters: there are multiple independent servers operating together to run tests from a single location.

To create a cluster, click the **Add to Cluster** link shown at the bottom of an Enterprise Agent's Settings. A dialog will open; choose to either add to a new cluster, or add to an existing cluster, and give the cluster a name. By default, the cluster will inherit the name of the first cluster member.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ef00be81c541c3517feb882d4ee152a3217ed048%2Fproduct-documentation\_enterprise-agents\_working-with-enterprise-agent-clusters-1.png?alt=media)

When the new cluster is created, all agent settings will be automatically mapped to the new cluster. This includes:

* Inherit all tests assigned to the standalone agent
* All accounts which had access to the standalone agent
* Agent groups where the standalone agent was a member
*
  * Verify SSL certificates setting
  * Agent notification rules selections
* For customers using the API, the cluster retains the agentId of the first agent added to the cluster

### Adding Capacity to a Cluster <a href="#adding-capacity-to-a-cluster" id="adding-capacity-to-a-cluster"></a>

Once a cluster is created, more agents can be added to the cluster, by running through the same process and clicking the add to existing cluster, then selecting the cluster.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8d97fc54ba600ab791b84de611206d2dbcac5ef7%2Fproduct-documentation\_enterprise-agents\_working-with-enterprise-agent-clusters-2.png?alt=media)

When adding a new agent to an existing cluster, the cluster will:

* Inherit all tests assigned to the agent
* Ignore all groups assigned to the newly assigned agent
* Enforce the cluster settings for:
  * Verify SSL certificates setting
* For customers using the API, the newly assigned agent's agentID will no longer exist

If a test on an inbound agent is already assigned to the cluster, one agent will appear as removed from the test.

To delete an Enterprise Agent cluster, navigate to

[Cloud & Enterprise Agents > Agent Settings > Clusters tab](https://app.thousandeyes.com/settings/agents/enterprise/?section=clusters)

. Expand the Enterprise Agent cluster's row, then click the trash icon in the lower left corner. Note that deleting a cluster with existing Enterprise Agent cluster members will also delete the Enterprise Agents. To preserve the Enterprise Agents, remove them from the cluster before deleting the cluster. See the section below for instructions on removing an agent from a cluster.

### Removing an Agent from a Cluster <a href="#removing-an-agent-from-a-cluster" id="removing-an-agent-from-a-cluster"></a>

In certain cases, an Administrator may want to remove an agent from a cluster. To accomplish this, under the Settings menu, select Enterprise Agents, and choose the Cluster tab. Expand the Enterprise Agent cluster's row, then click the **x** icon next to the cluster member. You'll be shown a confirmation dialog:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ccb0cedaf6c5c99d15e8c9bfe0a874b534ec3024%2Fproduct-documentation\_enterprise-agents\_working-with-enterprise-agent-clusters-3.png?alt=media)

Click the **Remove** button to remove the agent from the cluster and return the agent to a standalone status. This operation removes the agent, and recreates it in the context of the user's current account group, so be aware of your current account group, in the event that your user has management permissions across multiple account groups. The agent is created fresh, inheriting default Agent Notification rules, and without any tests assigned.

In the Enterprise Agents page, you'll be able to tell which agent is a cluster member by looking at the expanded agent details of an agent, or the cluster icon. Click the cluster hyperlink to open the cluster settings, and view other cluster members.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ac7833dc7017158ba2b3edabed6164aa28c2defb%2Fproduct-documentation\_enterprise-agents\_working-with-enterprise-agent-clusters-4.png?alt=media)

Utilization details for the agent are shown at the cluster member level, as well as on an overall basis at the cluster level.

It's important to note that Enterprise Agent clusters are not meant for high availability of agents. If a cluster member is shut down or becomes unreachable via the network while tests are assigned to it, those tests will remain assigned to that same agent (cluster member). Removing the agent from a cluster will force redistribution of those tests to other cluster members.

### Test Management and Utilization <a href="#test-management-and-utilization" id="test-management-and-utilization"></a>

New tests assigned to the cluster are distributed to each cluster member, based on each agent's utilization. As a new agent is assigned, the tests assigned to that agent are distributed amongst the cluster members.

If a cluster member agent is deleted, the tests assigned to the agent are redistributed amongst the remaining cluster members.

Utilization is shown for each agent in the agent settings page, and the overall cluster utilization shows the average value across all cluster members.

Views will show the name of the agent as the cluster name, but show the individual IP address of the cluster member. This may include private and/or public IP information, so to troubleshoot individual cluster members having problems resolving data on a test, you'll have to identify the cluster member assigned to the test, and diagnose from that specific agent. To view the information for a specific test, hover over the agent icon.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-79e1cae603f1d946069f823c7de3b457e015274f%2Fproduct-documentation\_enterprise-agents\_working-with-enterprise-agent-clusters-5.png?alt=media)

Using a cluster as a target for agent-to-agent tests will work fine, unless all agents are behind the same NAT. In this scenario, you'll need to create a firewall rule for the target, which would point to a specific agent in the cluster. While all results will behave as planned, the agent targeted will absorb all agent-to-agent tests targeted at that specific port on the cluster. To target different agents, change the port of the target, which is set under the Advanced Settings tab of the test's configuration.

Versions 5 and later of the ThousandEyes API have support for Enterprise Agent clusters. See

[http://developer.thousandeyes.com](http://developer.thousandeyes.com/)

for information on Enterprise Agent clusters in the context of our API.

* All agents must be owned by the same account group (i.e. use the same account token)
* All agents must be using the same address family (no mixing of IPv4 agents with IPv6 agents)
* Agents should be running the same version of both operating system and agent software
* Agents should have similar hardware configuration
* Agents should be in the same physical location
* Agents should be running the same components (ie, all agents run both agent and BrowserBot, or just agent)
