# Enterprise Agent System Requirements

This article details all system requirements required for installing a ThousandEyes Enterprise Agent.

Each Enterprise Agent will have different requirements based on the type of device (virtual appliance, physical appliance, Cisco device etc) the agent is being installed on, and the type of installation (Docker, linux package etc). Review the relevant sections for your Enterprise Agent/s before continuing with the installation process.

The table below outlines the key hardware requirements common to all Enterprise Agents, both with and without the BrowserBot component included.

The BrowserBot component performs page load and transaction tests.

| ​                   | **With BrowserBot** | **Without BrowserBot** |
| ------------------- | ------------------- | ---------------------- |
| CPU Count           | 2                   | 2                      |
| RAM                 | 2 GB                | 1 GB                   |
| Hard Disk Space     | 20 GB               | 20 GB                  |
| Network Interface   | Required            | Required               |
| Internet Connection | Required            | Required               |

For customers importing the virtual appliance in OVA format into VMware or Oracle VirtualBox, or importing the ZIP format into Microsoft Hyper-V, a serial port is included in the virtual machine definition. In most cases, if you are using these hypervisors you do not need to perform any additional configuration to meet this requirement.

For customers using hypervisors that may not support the OVA or ZIP templates, you should ensure that the configuration of the virtual machine provides a serial device for console access, prior to importing the virtual appliance.

### Supported Enterprise Agent Operating Systems <a href="#supported-enterprise-agent-operating-systems" id="supported-enterprise-agent-operating-systems"></a>

The ThousandEyes Enterprise Agent can be installed as a package on native Linux operating systems, as a ThousandEyes virtual appliance in a virtualized environment, as a physical appliance, or as a Docker container.

ThousandEyes supports installing the Enterprise Agent on the following operating systems:

* Red Hat Enterprise Linux and CentOS 7
* Red Hat Enterprise Linux 8

Enterprise Agents are supported on x64 (64-bit) architecture.

For customers running other distributions or versions of Linux, ThousandEyes recommends installing

[Docker](https://www.docker.com/why-docker)

on the Linux system, then installing the ThousandEyes Enterprise Agent Docker image.

Access to the latest point release software repositories for each supported OS version is required (i.e., an agent installed on RHEL 7.4 needs access to RHEL 7.x repositories).

There is currently no native version of the ThousandEyes Enterprise Agent software for Microsoft Windows. Customers running Windows may consider the following virtualization options:

*   Other Windows versions: Use a virtualization product such as Oracle's VirtualBox platform for virtualization to host a

    [ThousandEyes Virtual Appliance](https://docs.thousandeyes.com/product-documentation/enterprise-agents/how-to-set-up-the-virtual-appliance)

    . Check out

    [www.virtualbox.org](https://www.virtualbox.org/)

    for more details. Other virtualization software such as VMware Workstation can also run virtual appliance virtual machines.

An Ubuntu Linux operating system running in Microsoft's Windows Subsystem for Linux does not support Enterprise Agents.

There is currently no native version of the ThousandEyes Enterprise Agent for Mac OS X. Customers running Mac OS X with an Intel processor may consider the following virtualization options to host a

[ThousandEyes Virtual Appliance](https://docs.thousandeyes.com/product-documentation/enterprise-agents/how-to-set-up-the-virtual-appliance)

:

*   Oracle VirtualBox, a freely distributed hypervisor. Check out

    [www.virtualbox.org](https://www.virtualbox.org/)

    for more details.

#### Operating System Support Lifecycle <a href="#operating-system-support-lifecycle" id="operating-system-support-lifecycle"></a>

### Supported Virtual Appliance Platforms <a href="#supported-virtual-appliance-platforms" id="supported-virtual-appliance-platforms"></a>

ThousandEyes virtual appliances are based on Ubuntu LTS releases. New versions of the virtual appliance are made available when new versions of Ubuntu LTS are certified for the ThousandEyes Enterprise Agent. ThousandEyes currently provides virtual appliances for the following platforms:

* Hypervisors capable of importing an OVA, such as Oracle VirtualBox and VMware ESXi

ThousandEyes provides an installer image for Intel NUC mini-PCs, based on the same software as the ThousandEyes virtual appliance. ThousandEyes will make every effort to ensure that an upgrade path is provided, so that customers can stay on a supported appliance version. In some cases, customers will need to reinstall the appliance software in order to stay on a supported appliance version. Customers in this scenario will be contacted while the underlying operating system is in the **End of Installation Support** phase in order to ensure an orderly transition.
