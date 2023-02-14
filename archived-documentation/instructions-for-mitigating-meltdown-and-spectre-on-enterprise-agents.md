# Instructions for Mitigating Meltdown and Spectre on Enterprise Agents

As of February 22, 2018, updates for ThousandEyes Enterprise Agents have been made available and tested for the Meltdown and Spectre Version 1 and 2 vulnerabilities. This document outlines recommendations for mitigating vulnerabilities in Enterprise Agents deployed in customer environments. Follow the instructions below for each Enterprise Agent deployment type to apply security updates to your Enterprise Agents.

### Instructions by Agent Deployment and Environment <a href="#instructions-by-agent-deployment-and-environment" id="instructions-by-agent-deployment-and-environment"></a>

#### Linux Package Enterprise Agents Deployed in Virtual Environments <a href="#linux-package-enterprise-agents-deployed-in-virtual-environments" id="linux-package-enterprise-agents-deployed-in-virtual-environments"></a>

Customers who run their own hypervisor software must patch the hypervisor and the host operating system on which the hypervisor runs, in addition to the guest operating system running the Enterprise Agent. Check the information below for your host operating system and hypervisor, or consult your vendor's support resources for updates.

Customers who use cloud-based service providers to run virtual environments will typically be responsible for updating the operating systems of the guest virtual machines.

* Download and install patch
* Addresses side-channel analysis due to speculative execution
* Applies to VMware products
  * Workstation / Workstation Pro
* Download and install patch
* Addresses Hypervisor-Assisted Guest Remediation for speculative execution issue
* Applies to VMware products
  * Workstation / Workstation Pro
* For Agents deployed in Hyper-V environments Windows Server will need to be updated first. Once the Server has been updated Hyper-V's registries will need to be modified to stop VM to VM and VM to host attacks. Refer to instructions linked above.

| Version                                                 | Article Showing updates and patches                                                           |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| Windows Server, version 1709 (Server Core Installation) | <p>​</p><p><a href="https://support.microsoft.com/en-us/help/4056892">4056892</a></p><p>​</p> |
| Windows Server 2016                                     | <p>​</p><p><a href="https://support.microsoft.com/en-us/help/4056890">4056890</a></p><p>​</p> |
| Windows Server 2012 R2                                  | <p>​</p><p><a href="https://support.microsoft.com/en-us/help/4056898">4056898</a></p><p>​</p> |
| Windows Server 2012                                     | Not available                                                                                 |
| Windows Server 2008 R2                                  | <p>​</p><p><a href="https://support.microsoft.com/en-us/help/4056897">4056897</a></p><p>​</p> |
| Windows Server 2008                                     | Not available                                                                                 |

**Amazon Web Services (AWS)**

* Underlying virtualization infrastructure should be patched for Meltdown and Spectre
* Customers are still responsible to update OS kernels for their hosts
* Underlying virtualization infrastructure should be patched for Meltdown and Spectre
* Customers are still responsible to update OS kernels for their hosts
* Underlying virtualization infrastructure should be patched for Meltdown and Spectre
* Customers are still responsible to update OS kernels for their hosts

For virtualized operating systems, follow instructions found under _Linux Package Enterprise Agents deployed in physical environments._

#### Linux Package Enterprise Agents Deployed in Physical Environments <a href="#linux-package-enterprise-agents-deployed-in-physical-environments" id="linux-package-enterprise-agents-deployed-in-physical-environments"></a>

Here's the quick & easy version:

$ sudo apt-get dist-upgrade

\*refer to patch notes to check if your kernel version has been patched.

**Red Hat Enterprise Linux and CentOS**

*
  * kernel-2.6.32-696.18.7.el6
*
  * kernel-3.10.0-693.11.6.el7

You can check your current kernel version with "uname -rs"

Linux 2.6.32-696.3.1.el6.x86\_64

If your kernel is not currently patched you can retrieve the latest updates with "yum update". Once run, check that a patched kernel has been loaded with "rpm -qa | grep kernel" - then reboot to apply the update.

kernel-firmware-2.6.32-696.18.7.el6.noarch

kernel-2.6.32-642.11.1.el6.x86\_64

dracut-kernel-004-409.el6\_8.2.noarch

kernel-2.6.32-696.3.1.el6.x86\_64

kernel-headers-2.6.32-696.18.7.el6.x86\_64

kernel-2.6.32-696.18.7.el6.x86\_64

kernel-2.6.32-642.15.1.el6.x86\_64

kernel-2.6.32-642.el6.x86\_64

After the reboot, run "uname -rs" once again to verify the new kernel has been loaded.

Linux 2.6.32-696.18.7.el6.x86\_64

#### ThousandEyes Virtual and Physical Appliances <a href="#thousandeyes-virtual-and-physical-appliances" id="thousandeyes-virtual-and-physical-appliances"></a>

The latest security updates from Ubuntu should have been applied to your Appliances automatically. Since this change affects the kernel, customers will be required to reboot the Agent. Review the article

[Rebooting ThousandEyes Appliances for Spectre and Meltdown mitigation](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA0440000009Sa6CAE)

for more information on the proper way to verify that the kernel has been updated and actions required.

#### ThousandEyes Enterprise Agents Deployed as Docker Containers <a href="#thousandeyes-enterprise-agents-deployed-as-docker-containers" id="thousandeyes-enterprise-agents-deployed-as-docker-containers"></a>

Due to Docker's design, which shares the kernel of the container with the host, there are no upgrades needed within deployed Docker containers. Please refer to appropriate operating system documentation in order to update the host's underlying operating system.

We do not expect a significant performance impact based on testing done in our lab environment. See

[this link](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA0440000009STUCA2)

for information showing details on the nominal performance impact.

This article will be updated as more updates are made available.
