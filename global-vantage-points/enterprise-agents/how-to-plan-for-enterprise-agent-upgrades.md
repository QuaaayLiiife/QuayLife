# How to Plan for Enterprise Agent Upgrades

### Recent Announcements for End of Operating System Support <a href="#recent-announcements-for-end-of-operating-system-support" id="recent-announcements-for-end-of-operating-system-support"></a>

The following operating systems are entering "end-of-life" status in 2021 according to their respective developers:

ThousandEyes will no longer provide software updates and support for these agents in 2021 as detailed by the table below:

| Operating System                                     | End of Installation Support | End of Support by Customer Engineering | End of Life     |
| ---------------------------------------------------- | --------------------------- | -------------------------------------- | --------------- |
| Ubuntu 16.04                                         | January 31st                | April 30th                             | August 15th     |
| Red Hat Enterprise Linux / CentOS / Oracle Linux 7.6 | Feburary 28th               | May 31st                               | July 31st       |
| Red Hat Enterprise Linux / CentOS / Oracle Linux 7.7 | May 31st                    | August 30th                            | October 31st    |
| CentOS 8.2                                           | October 2nd                 | December 31st                          | March 1st, 2022 |
| CentOS 8.3                                           | October 2nd                 | December 31st                          | March 1st, 2022 |
| CentOS 8.4                                           | October 2nd                 | December 31st                          | March 1st, 2022 |

When agents reach end-of-life they will no longer be able to connect to our platform.

### Identify Agents that Require Upgrades <a href="#identify-agents-that-require-upgrades" id="identify-agents-that-require-upgrades"></a>

You may identify which of your agents are running on an unsupported Operating System from the

[Agent Settings](https://app.thousandeyes.com/settings/agents/enterprise/?section=agents)

page.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f882fe67be208f0bf13bf1a7531582b363b4604d%2Fproduct-documentation\_enterprise-agents\_how-to-plan-for-enterprise-agent-upgrades-1.png?alt=media)

To identify agents requiring an upgrade:

1.  1\.

    A red triangle (attention) icon will be located next to the name of each agent which requires attention.
2.  2\.

    Hovering over an agent's attention icon will display a list of items to be addressed. Agents requiring an upgrade will display the message "**Agent OS will soon be unsupported"**

When communicating with your team members which agents need to be updated, the following will be useful:

**3. Agent Name:** This is the name used by the ThousandEyes platform and may not match the hostname of the system running the Enterprise Agent

**4. Agent IP Addresses:** This includes both public and private IP addresses

**5. Agent Operating System:** This includes both distribution and version number

**6. Agent Installation Type:** This may be Linux Package, Docker, physical appliance, or virtual appliance

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5ced355469e766fff9139acf3a19b3308da7d156%2Fproduct-documentation\_enterprise-agents\_how-to-plan-for-enterprise-agent-upgrades-2.png?alt=media)

The following will be useful for verifying the agent's configuration post-upgrade:

**7.** **Target for Tests:** This may be either an IP Address or a domain name

**8. Proxy Settings:** An information icon will appear if your agent is using a proxy

### Upgrade Paths for Specific Systems <a href="#upgrade-paths-for-specific-systems" id="upgrade-paths-for-specific-systems"></a>

Customers who choose to install the ThousandEyes Enterprise Agent onto their own Linux system are responsible for system maintenance.

ThousandEyes has tested and documented the upgrade process for supported Linux distributions. The following information may be used as a general guideline for customers to reference when planning upgrades.

**Red Hat Enterprise Linux 7.x, CentOS 7.x**

RHEL 7 and CentOS 7 systems may be updated to version 7.9 using the following command:

Custom repositories should be made current prior to the upgrade.

Canonical has provided an upgrade path from Ubuntu 16.04 to Ubuntu 18.04. Please note that only 64-bit operating systems are supported.

#### ThousandEyes Virtual Appliances <a href="#thousandeyes-virtual-appliances" id="thousandeyes-virtual-appliances"></a>

ThousandEyes has provided an automated upgrade path for customers to update their virtual appliance. The upgrade process requires SSH access to the appliance.

Complete instructions for upgrading a ThousandEyes appliance are available

[here](https://docs.thousandeyes.com/product-documentation/enterprise-agents/upgrade-ubuntu-16.04-xenial-based-thousandeyes-appliances)

.

#### ThousandEyes Physical Appliances <a href="#thousandeyes-physical-appliances" id="thousandeyes-physical-appliances"></a>

ThousandEyes has provided an automated upgrade path for customers who wish to update their physical appliance. This upgrade process requires SSH access to the appliance.

Complete instructions for upgrading a ThousandEyes appliance are available

[here](https://docs.thousandeyes.com/product-documentation/enterprise-agents/upgrade-ubuntu-16.04-xenial-based-thousandeyes-appliances)

.

The current Docker container is built using the base Ubuntu 18.04 container image. Currently, no upgrade is necessary.

#### Cisco Switch Virtual Appliances <a href="#cisco-switch-virtual-appliances" id="cisco-switch-virtual-appliances"></a>

### Replacing Enterprise Agents <a href="#replacing-enterprise-agents" id="replacing-enterprise-agents"></a>

#### ThousandEyes Enterprise Agents May Be Replaced Using Two Different Methods <a href="#thousandeyes-enterprise-agents-may-be-replaced-using-two-different-methods" id="thousandeyes-enterprise-agents-may-be-replaced-using-two-different-methods"></a>

This method consists of deploying a new agent, clustering together the new agent with the old one, and then deleting the old agent from the cluster. The act of clustering transfers test associations and agent characteristics.

Complete instructions for replacing Enterprise Agents using the agent clustering method are available

[here](https://docs.thousandeyes.com/product-documentation/enterprise-agents/replacing-an-enterprise-agent-using-the-agent-clustering-method)

.

#### Transferring Agent Identity Files <a href="#transferring-agent-identity-files" id="transferring-agent-identity-files"></a>

During the installation of a replacement Enterprise Agent, identity files from an existing Enterprise Agent are transferred to the replacement system. The platform will make no distinction between the original agent and the replacement agent.

Complete instructions for replacing Enterprise Agents using agent identity files are available

[here](https://docs.thousandeyes.com/product-documentation/enterprise-agents/replacing-an-enterprise-agent-using-agent-identity-files)

.

### Requesting support consultations <a href="#requesting-support-consultations" id="requesting-support-consultations"></a>

Some customers may use the upgrade process as an opportunity to consider new agent deployment options, such as replacing virtual machines with containers. ThousandEyes Customer Engineering is available via our

[in-application chat function](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes)

, or via email at

\[email protected]

to answer any questions that you may have.
