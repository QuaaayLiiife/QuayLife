# Getting Started with Enterprise Agents

ThousandEyes Enterprise Agents provide you with an "inside-out" or "inside-in" vantage point for insights into the performance and dependencies of your application, regardless of how the application is delivered (internal to your datacenter, as SAAS, or from a third-party datacenter).

This article helps you get started with deploying Enterprise Agents to your environment.

For this guide, we assume you have read the previous getting started guide sections:

This getting started guide introduces the following concepts, procedures, and best practices for deploying Enterprise Agents:

Enterprise Agents should be placed where you want to run your test. For example, if you want to monitor your SAAS applications, Enterprise Agents should be placed at all significant concentrations of users. In most cases, this means that each office will have a single Enterprise Agent. For some very large campuses, multiple agents can be deployed to monitor different parts of the campus.

Unless your requirements dictate that you have floor and/or VLAN-based visibility, it is not usually necessary to install an Enterprise Agent on every floor of an office.

If ThousandEyes is used for monitoring application dependencies, such as external APIs, you should deploy an Enterprise Agent in the same datacenter as the application. This will allow you to configure tests to the external API and quickly isolate issues.

The following sections cover installing an agent for monitoring user applications from campus locations.

#### Placement Inside the Location <a href="#placement-inside-the-location" id="placement-inside-the-location"></a>

The Enterprise Agent should be placed as close to the users as possible. Deploying the agent on an access switch, such as the Cisco Catalyst 9300, is a very efficient way to achieve that goal. If an access switch is not an option for deployment, you can use any deployment method mentioned in the

[Enterprise Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents)

documentation, taking into consideration that the agent should be deployed as close to the users as possible.

#### Choosing the Right Network <a href="#choosing-the-right-network" id="choosing-the-right-network"></a>

For most use cases, the best network to install the agent on is the same network as the user. This ensures that all dependencies that a user has (such as QoS policies, firewall policies, and routing) are also applicable to the ThousandEyes test traffic.

If multiple networks with distinct traffic policies exist (such as "users", "guests", and "voice"), multiple test sources will be needed. This can be achieved by either deploying multiple Enterprise Agents, or by configuring the multi-interface function.

### Adding a New Enterprise Agent <a href="#adding-a-new-enterprise-agent" id="adding-a-new-enterprise-agent"></a>

To add an Enterprise Agent:

1.  1\.

    Log into the ThousandEyes web application.
2.  2\.

    Navigate to **Cloud & Enterprise Agents > Agent Settings > Enterprise Agents > Agents**:

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9bd1d68a5c0389cbe2b19a1ebdb288cdaab57289%2Fproduct-documentation-getting-started-getting-started-with-enterprise-agents-1.png?alt=media)

    Enterprise Agent Settings
3.  3\.

    Click **Add New Enterprise Agent**. If this button is not visible, you'll need to review your user permissions. For more information, see

    [Role-Based Access Control](https://docs.thousandeyes.com/product-documentation/user-management/rbac/role-based-access-control-explained)

    .

    After clicking the button, the installation menu panel will appear. This panel displays the installation options, system requirements, and the account group token, and links to the specific installation guides for each method.

    **Note:** The _account group token_ is the unique key that links an Enterprise Agent to a ThousandEyes account group. Treat this token like a password.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1526d8ebd8c1c47611859e8e3b043216128fd241%2Fproduct-documentation-getting-started-getting-started-with-enterprise-agents-2.png?alt=media)

    Add New Enterprise Agent dialog
4.  4\.

    Follow the steps in the installation guide for your deployment method. When your new agent is successfully added, it will appear in the **Enterprise Agents > Agents** view.

    The **Status/Last Contact** column will show a green circle icon and the **Just Now** status for your newly created Enterprise Agent.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b90fd301db666c91ad4d15644a9070ee3acf6428%2Fproduct-documentation-getting-started-getting-started-with-enterprise-agents-3.png?alt=media)

    Enterprise Agent list showing new agents

Your Enterprise Agent is now ready to use. We recommend you take the following steps with all new agents:

* Give them a descriptive agent name and hostname, to ensure they are easily identifiable.
* Add them to a single account group, then share them with other account groups for use in tests.

ThousandEyes views assigning all Enterprise Agents to a single account group and sharing them with other account groups for use in specific tests as the best practice. This is because it ensures one team is responsible for managing all agents.

Enterprise Agents do not consume any licenses. It is the tests running on those agents that consume units. For more information, see

[How Unit Consumption Works](https://docs.thousandeyes.com/product-documentation/user-management/usage-and-billing/how-unit-consumption-works)

.

Some Cisco platforms include ThousandEyes units as part of their license, as outlined in the

[Cisco Device Entitlements](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/cisco-devices#entitlements)

section.

Enterprise Agents need to connect to the ThousandEyes platform to function, and they need to be able to perform tests that send detailed output to the platform.

All communication with the ThousandEyes platform from the Enterprise Agent is initiated by the agent, and so there is no requirement to configure inbound access from the ThousandEyes platform to the Enterprise Agent.

Network access for testing is dependent on the test type configured. For example, an HTTP test requires different ports and protocols than a DNS or voice test. For more information about test types, see

[Getting Started with Tests](broken-reference)

.

In order for the path visualization to properly function, you will need to allow ICMP error messages inbound to the Enterprise Agents. If a well-behaved stateful firewall is used, this should work automatically if outbound traffic is permitted, but in some cases, specific access will need to be configured.

The exact destination and protocols depend on your installation type, the tests performed, and the ThousandEyes region your account is provisioned in. For detailed firewall configuration requirements, see

[Firewall Configuration for Enterprise Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/configuring/firewall-configuration-for-enterprise-agents)

.

When you configure a test, you can use an agent label to assign multiple agents to that test. This makes agent selection easier, and ensures testing is configured consistently. In addition, these labels can be used to make dynamic dashboards that automatically adjust when the testing changes.

The same label can be applied to both Cloud and Enterprise Agents, and multiple labels can be applied to the same agent.

We recommend that you use labels to group similar agents together. For example, you could add labels for network segments (like "LAN", "VOICE", or "GUEST"), locations (countries, cities, regions etc), or internal classifications (like "Large Branch", "Datacenter" etc). You could also create labels specifically for Cloud Agents, such as a label for all agents used to monitor global websites and another for regional locations etc.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f0ec7a276e6d283c9ddbb448fc5cd470220e54f9%2Fproduct-documentation-getting-started-getting-started-with-enterprise-agents-4.png?alt=media)

### Sharing Enterprise Agents Across Account Groups <a href="#sharing-enterprise-agents-across-account-groups" id="sharing-enterprise-agents-across-account-groups"></a>

As previously mentioned, ThousandEyes best practice is to assign all Enterprise Agents to a single account group, and share access to the account groups that will be using the agents for testing, as shown in the following example:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5aa10a82623617ee532a1729f319bc6fb674b2b4%2Fproduct-documentation-getting-started-getting-started-with-enterprise-agents-5.png?alt=media)

By deploying agents this way, you ensure that there is a single place in the platform where all Enterprise Agents are visible, making management of these agents easier and more consistent, while maintaining control over who can initiate tests from individual agents.

### Setting Up Agent Notifications <a href="#setting-up-agent-notifications" id="setting-up-agent-notifications"></a>

Now that your Enterprise Agents are up and running, you will want to ensure they remain in a healthy state. One way to achieve this is to make sure you receive notifications when an error condition occurs.

Notification rules for Enterprise Agent conditions can be configured from the **Cloud & Enterprise Agents > Agent Settings > Enterprise Agents > Notifications** page of the ThousandEyes web application.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c788e2c51f3e754aeeaebdb6d943ad1677d9bc4e%2Fproduct-documentation-getting-started-getting-started-with-enterprise-agents-6.png?alt=media)

These notification rules/conditions can be set for:

* Clock offset for an agent.
* Agent software being outdated.

### Analyzing Agent Utilization <a href="#analyzing-agent-utilization" id="analyzing-agent-utilization"></a>

Each test running on a ThousandEyes Enterprise Agent is assigned dedicated time in the test queues belonging to the agent. An Enterprise Agent can only run one task per queue at a time. This mechanism ensures that each test has dedicated resources, and that multiple tests won't interfere with each other.

Agent utilization is mostly dependent on server response times and queue utilization, so it will not help to add more resources to an overloaded agent. Adding more members to a cluster, or removing unnecessary tests, are the only ways to reduce agent load.
