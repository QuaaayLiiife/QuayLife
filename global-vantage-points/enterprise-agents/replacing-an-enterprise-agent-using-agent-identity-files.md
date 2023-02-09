# Replacing an Enterprise Agent Using Agent Identity Files

ThousandEyes Enterprise Agents can be replaced by using one of the following methods:

1.  1\.

    This method consists of deploying a new agent, clustering together the new agent with the old one, and then deleting the old agent from the cluster. The act of clustering transfers test associations and agent characteristics. Detailed instructions for this method are available in

    [Replacing an Enterprise Agent Using the Agent Clustering Method](https://docs.thousandeyes.com/product-documentation/enterprise-agents/replacing-an-enterprise-agent-using-the-agent-clustering-method)

    )
2.  2\.

    **Transferring Agent Identity Files:**

    During the installation of a replacement Enterprise Agent, identity files from an existing Enterprise Agent are transferred to the replacement system. The platform will make no distinction between the original agent and the replacement agent.

This document will demonstrate how to successfully transfer Enterprise Agent identity files from an existing to a newly deployed agent.

### Enterprise Agent Identity Files <a href="#enterprise-agent-identity-files" id="enterprise-agent-identity-files"></a>

The Enterprise Agent software package is installed as a service named `te-agent` onto a

[supported Linux operating system](https://docs.thousandeyes.com/product-documentation/enterprise-agents/supported-enterprise-agent-operating-systems)

. The following three files are used by the `te-agent` service during operation and must be transferred from the original agent to the replacement agent:

* This is the agent's main configuration file and contains account group information, logging, and proxy settings
* During service start, `te-agent` reads this file and applies configuration settings
* This file is not unique to a specific agent and may be re-used to configure identical settings to multiple agents

**/var/lib/te-agent/te-agent-config.sqlite**

* This file contains the agent ID, collector assignment, and current runtime configuration settings
* Information within this file is used to authenticate with the ThousandEyes platform
* **WARNING: This file is unique to the agent and must not be used by two agents at the same time. DO NOT copy this file to more than one replacement Agent.**

**/var/lib/te-agent/te-agent.sqlite**

* This file contains the not-yet-submitted test and device layer data
* **WARNING: This file is unique to the agent and must not be used by two agents at the same time. DO NOT copy this file to more than one replacement Agent.**

### Obtaining Identity Files from the Original Agent <a href="#obtaining-identity-files-from-the-original-agent" id="obtaining-identity-files-from-the-original-agent"></a>

#### Disable the Original Enterprise Agent Using the ThousandEyes Web Application <a href="#disable-the-original-enterprise-agent-using-the-thousandeyes-web-application" id="disable-the-original-enterprise-agent-using-the-thousandeyes-web-application"></a>

Prior to obtaining Enterprise Agent identity files, it is recommended to temporarily disable the Enterprise Agent to be replaced:

**1.** Review the list of active Enterprise Agents for the name of the agent to be replaced **2.** Click the **options** button in the right-hand side of the agent information row and select **Disable**

#### Stop and Disable the Original Enterprise Agent Service <a href="#stop-and-disable-the-original-enterprise-agent-service" id="stop-and-disable-the-original-enterprise-agent-service"></a>

ThousandEyes service must be stopped on your original agent before you may copy identity files. Disabling the service will prevent the decommissioned agent from communicating with the ThousandEyes platform in the event that the VM is restarted.

**Operating systems using systemd (Ubuntu 16.04+, RHEL & CentOS 7+):**

$ sudo sytemctl stop te-agent.service

$ sudo systemctl disable te-agent.service

$ sudo service te-agent stop

$ sudo chkconfig te-agent off

$ sudo update-rc.d -f te-agent remove

#### Copy Enterprise Agent Identity Files to a Single Directory <a href="#copy-enterprise-agent-identity-files-to-a-single-directory" id="copy-enterprise-agent-identity-files-to-a-single-directory"></a>

Copy identity files to a single directory for ease of management:

$ sudo mkdir \<directory\_name>

$ sudo cp /var/lib/te-agent/\*.sqlite \~/\<directory\_name>

$ sudo cp /etc/te-agent.cfg \~/\<directory\_name>

#### Compress the Directory Containing Your Original Agent Identity Files <a href="#compress-the-directory-containing-your-original-agent-identity-files" id="compress-the-directory-containing-your-original-agent-identity-files"></a>

Compress the directory containing copied identity files for ease of transfer

$ sudo zip -r \<directory\_name>.zip \<directory\_name>

#### Delete the Agent Identity Files From Your Original Agent <a href="#delete-the-agent-identity-files-from-your-original-agent" id="delete-the-agent-identity-files-from-your-original-agent"></a>

While the original Identity files will be deleted when the VM is destroyed, it is always possible that the VM could be restarted prior to deletion. Removing these files safeguards from errors associated with two agents connecting to the platform with the same agent ID.

original-agent$ sudo rm /etc/te-agent.cfg

original-agent$ sudo rm /var/lib/te-agent/\*.sqlite

### Transferring Identity Files <a href="#transferring-identity-files" id="transferring-identity-files"></a>

#### Use SCP to Transfer Files Between Agents <a href="#use-scp-to-transfer-files-between-agents" id="use-scp-to-transfer-files-between-agents"></a>

From your new replacement agent's terminal, you may use the following command to obtain files from your original agent (provided the original and the new Enterprise Agent can communicate with each other directly):

$ scp \<user>@\<original-agent-IP>:\~/\<directory\_name>.zip \~

Alternatively, from your original agent's terminal you may use the following command to transfer files to your replacement agent:

$ scp \~/\<directory\_name>.zip \<user>@\<replacement-agent-IP>:\~

**NOTE:** You only need to copy the .zip file once.

### Installing a Replacement Agent Using Transferred Identity Files <a href="#installing-a-replacement-agent-using-transferred-identity-files" id="installing-a-replacement-agent-using-transferred-identity-files"></a>

#### Install the ThousandEyes Repository <a href="#install-the-thousandeyes-repository" id="install-the-thousandeyes-repository"></a>

You will use the ThousandEyes repository to download and install Enterprise Agent services:

$ sudo apt-get install software-properties-common

$ sudo apt-add-repository https://apt.thousandeyes.com/

$ sudo yum-config-manager --add-repo https://yum.thousandeyes.com/RHEL/7/x86\_64

$ sudo yum-config-manager --add-repo https://yum.thousandeyes.com/CentOS/7/x86\_64

#### Install the ThousandEyes Repository GPG Key <a href="#install-the-thousandeyes-repository-gpg-key" id="install-the-thousandeyes-repository-gpg-key"></a>

You must install the ThousandEyes repository GPG key in order to validate the authenticity of downloaded packages:

$ sudo wget -q https://apt.thousandeyes.com/thousandeyes-apt-key.pub

$ sudo apt-key add thousandeyes-apt-key.pub

$ sudo rpm --import https://yum.thousandeyes.com/RPM-GPG-KEY-thousandeyes

#### Update Your Operating System's Package Manager <a href="#update-your-operating-systems-package-manager" id="update-your-operating-systems-package-manager"></a>

Pulling the repository metadata verifies that the ThousandEyes repository and corresponding GPG key are properly installed:

$ sudo yum clean metadata

#### Install the ThousandEyes Enterprise Agent Using Your OS's Package Manager <a href="#install-the-thousandeyes-enterprise-agent-using-your-oss-package-manager" id="install-the-thousandeyes-enterprise-agent-using-your-oss-package-manager"></a>

The `te-agent` package and service are what constitutes the heart of an Enterprise Agent. The

[BrowserBot](https://docs.thousandeyes.com/product-documentation/enterprise-agents/what-is-browserbot)

component (the `te-browserbot` package and service) is a component that performs browser-based tests.

$ sudo apt-get install te-agent te-browserbot

$ sudo yum install te-agent te-browserbot

#### Decompress the Original Agent Identity Files Within Your Replacement System <a href="#decompress-the-original-agent-identity-files-within-your-replacement-system" id="decompress-the-original-agent-identity-files-within-your-replacement-system"></a>

Once decompressed, a directory with the same name as the directory from your original agent will be available:

$ unzip \<directory\_name>.zip

#### Copy the Agent Identity Files to the Target Directories Within Your Replacement System <a href="#copy-the-agent-identity-files-to-the-target-directories-within-your-replacement-system" id="copy-the-agent-identity-files-to-the-target-directories-within-your-replacement-system"></a>

Copy the agent identity files to their final location:

$ sudo cp \<directory\_name>/\*.sqlite /var/lib/te-agent

$ sudo cp \<directory\_name>/te-agent.cfg /etc

#### Start and Enable Enterprise Agent Services <a href="#start-and-enable-enterprise-agent-services" id="start-and-enable-enterprise-agent-services"></a>

Starting agent services will activate the ThousandEyes agent. Enabling a service ensures that it will start during system boot. To start and enable relevant services, execute the following commands:

$ sudo systemctl start te-agent.service

$ sudo systemctl start te-browserbot.service

$ sudo systemctl enable te-agent.service

$ sudo systemctl enable te-browserbot.service

Once your replacement agent has been brought online, you may re-enable your agent within the ThousandEyes web application:

**1.** Review the list of active Enterprise Agents for the name of the agent that was replaced. **2.** Click the options button in the right-hand side of the agent information row and select **Enable**.

Upon completion, review the **Advanced Settings** section to ensure that the agent information is correct:

Select the **Advanced Settings** tab of your Enterprise Agent information pane:

**1.** Verify that your Enterprise Agent is checking into the platform regularly **2.** Verify that the IP address and listed Operating System are correct **3.** Review the proxy settings (if applicable) to verify that they are correct
