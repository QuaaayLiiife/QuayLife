# Enterprise Agent Installation on Juniper NFX Routers

This article details the steps to install the ThousandEyes Virtual Appliance (VA) as a third-party virtual machine on a

[Juniper NFX](https://www.juniper.net/documentation/en\_US/release-independent/junos/information-products/pathway-pages/nfx-series/product/index.html)

router. The NFX series supports Juniper's

[Virtual Network Functions](https://www.juniper.net/documentation/en\_US/cso1.0/topics/concept/nsd-vnf-overview.html)

(VNF). A VNF virtual machine provides all the needed functionality for a fully virtualized networking environment.

* Junos OS Release 15.1X53-D45 or higher
* Minimum 8 GB of physical memory
* 2 GB of virtual memory per ThousandEyes Virtual Appliance
* Internet connectivity from the Juniper Device Manager

First configure network settings in Junos OS, consisting of a VLAN containing a physical network interface, and a bridged virtual interface belonging to the VNF containing the ThousandEyes Virtual Appliance. Then use the JDM to install and configure the ThousandEyes VNF. In our example we are going to use VLAN 100, physical interface GigabitEthernet 0/0/1, virtual bridge interface SXE 0/0/0 and "ThousandEyesVNF" as the name of our VNF.

The installation process for a ThousandEyes Virtual Appliance VNF consists of 3 steps:

1.  1\.

    Configuring Network Settings
2.  2\.

    Installing and activating the ThousandEyes Virtual Appliance
3.  3\.

    Initializing the Virtual Appliance

### Configure Network Settings <a href="#configure-network-settings" id="configure-network-settings"></a>

To enable the connectivity between the VA and the physical network (LAN) a physical network interface (Ethernet interface) must be bridged with an internal-facing interface (SXE interface) using a routing instance named host-os and a VLAN.

Perform the following steps to configure the interface bridging:

1.  1\.

    Connect to the router's JDM command line interface as the root user

    The connection can be made using a console port or via network login (SSH or telnet). The example below connects using SSH.

    Last login: Sun Oct 23 13:35:46 2016 from 10.100.10.239
2.  2\.

    Connect to the Junos Control Plane (JCP) and enter the JCP command line interface. The JCP provides access to Junos OS and is implemented in a VNF virtual machine called vjunos0. The example below connects using SSH.

    Last login: Wed Oct 19 11:10:20 2016 from 192.168.1.254

    \--- JUNOS 15.1X53-D47.4 Kernel 64-bit FLEX JNPR-10.3-20170523.350481\\\_build
3.  3\.

    Entering configuration mode
4.  4\.

    Configure the VLAN to be used on the physical network (LAN). The example below uses a VLAN name of vlan100 and a VLAN ID of 100.

    root\\# set vlans vlan100 vlan-id 100
5.  5\.

    Configure a physical network port (front panel port) and add it to the VLAN. The example below uses a gigabit Ethernet port ge-0/0/1.

    root\\# set interfaces ge-0/0/1 unit 0 family ethernet-switching vlan members vlan100
6.  6\.

    Configure an internal network port as a trunk and add it to the VLAN. The example below uses an internal interface sxe-0/0/0. This interface normally should be a trunk interface in order to support traffic from multiple physical network ports.

    root\\# set interfaces sxe-0/0/0 unit 0 family ethernet-switching interface-mode trunk

    root\\# set interfaces sxe-0/0/0 unit 0 family ethernet-switching vlan members vlan100
7.  7\.

    Save the configuration using the commit command and return to the JDM

    Exiting configuration mode
8.  8\.

    Connect to the JDM and enter configuration mode

    Entering configuration mode
9.  9\.

    Assign the previously configured VLAN name to the host-os routing instance:

### Installing and Activating the ThousandEyes Virtual Appliance <a href="#installing-and-activating-the-thousandeyes-virtual-appliance" id="installing-and-activating-the-thousandeyes-virtual-appliance"></a>

1.  2\.

    Copy the file onto the Juniper NFX Series using one of the following methods:

    * Secure Copy Protocol (SCP)

    **Note:** By default, Juniper saves third-party containers to the /var/third-party/images folder.
2.  3\.

    In the JDM, configure the memory size of the VNF. We recommend at least 2 gigabytes of RAM per ThousandEyes Virtual Appliance.

    \[email protected]\\# set virtual-network-functions ThousandEyesVNF memory size 2097152

    \[email protected]\\# set virtual-network-functions ThousandEyesVNF memory features hugepages

    **Note:** If the JDM does not already have

    [hugepages](https://www.juniper.net/documentation/en\_US/junos/topics/reference/configuration-statement/hugepages-edit-virtual-network-functions.html)

    configured, configure the system memory:

    In this example, we configure 5 hugepages with 1 gigabyte of memory each. 1 hugepage is reserved for the JDM and the other 4 hugepages for the user's VNFs. 2 VNFs with 2 gigabytes of memory or 4 VNFs with 1 gigabyte of memory are two possible configurations, based on this example. Configure the actual number of total gigabytes as needed.
3.  4\.

    Assign a name to our new VNF and select the Virtual Appliance location. In this example, we use the name ThousandEyesVNF and a file path of /var/third-party/images/thousandeyes-va-64-16.04.juniper-ch1.qcow2.

    root\\# set virtual-network-functions ThousandEyesVNF image /var/third-party/images/thousandeyes-va-64-16.04.juniper-ch1.qcow2
4.  5\.

    Add the quantity of CPUs to be used and CPU hardware features. In this example, two CPUs with hardware virtualization enabled are added.

    root\\# set virtual-network-functions ThousandEyesVNF virtual-cpu 0 physical-cpu 4

    root\\# set virtual-network-functions ThousandEyesVNF virtual-cpu 1 physical-cpu 10

    root\\# set virtual-network-functions ThousandEyesVNF virtual-cpu count 2

    root\\# set virtual-network-functions ThousandEyesVNF virtual-cpu features hardware-virtualization
5.  6\.

    Configure the ThousandEyes Virtual Appliance interface. Select the interface eth2 because the interfaces eth0 and eth1 are reserved by Juniper NFX Series for management purposes.

    root\\# set virtual-network-functions ThousandEyesVNF interfaces eth2 mapping vlan members vlan100
6.  7\.

    Save and activate the Virtual Appliance
7.  8\.

    Verify that the ThousandEyes Virtual Appliance is running

    \## ID Name State Liveliness

    44 ThousandEyesVNF Running alive

### Initializing the ThousandEyes Virtual Appliance <a href="#initializing-the-thousandeyes-virtual-appliance" id="initializing-the-thousandeyes-virtual-appliance"></a>

1.  1\.

    Connect to the ThousandEyes Virtual Appliance's console

    You should see a console with the current Agent’s IP address as follows:

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e609dfe3ee4fa3b609fea3d072c7e2c8a7a1ef98%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-1.png?alt=media)

    ​

    If a different IP address is needed, type the “N” key, and enter the information to change the Network configuration.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-be0b1669500dbfe12cf907f5477768a9b5f5a720%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-2.png?alt=media)

    ​

    To exit the console press “CTRL + SHIFT + ] ”
2.  2\.

    Access the ThousandEyes Virtual Appliance

    Using a web browser from a system on the LAN, access the ThousandEyes Virtual Appliance using the URL and login credentials shown in the console screen.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5eea7530be906aaa3d16252218439f90e2aa5db3%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-3.png?alt=media)

    ​
3.  3\.

    Change the Web Interface password

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2e81360eb1807b41185219d03195b545cfc4df18%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-4.png?alt=media)

    ​
4.  4\.

    Obtain and enter the Account Group Token

    Click the **ThousandEyes Platform Account Settings** link.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d7c6d317cc599a6b8c6e8ff1e6b681d16ba71b49%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-5.png?alt=media)

    ​

    From the

    [Settings > Enterprise Agents](https://app.thousandeyes.com/settings/agents/enterprise/?section=agents)

    page, open the **Add New Agent** form and click the **Show Account Group Token for Installation** link, at the bottom.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8467d09bb4548b7f6c17db01450b665018f11a42%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-6.png?alt=media)

    ​

    Copy the Token and paste into the **Account Token** field of the ThousandEyes Virtual Appliance Setup.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fe00b88dc0fbd3fab069dc19f47c357896d0723e%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-7.png?alt=media)

    ​

    Select 'Yes' to install the BrowserBot component if using Page Load or Transaction tests, then click the **Next** button. If the Diagnostics check is successful, the Virtual Appliance's Status page should indicate that the ThousandEyes Agent is running.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-80ece08020883f10e6393263a5a4bd8276db0b9d%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-8.png?alt=media)

    ​

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bf9a8c913685e89aaf1ea442cbf91b20144f59ee%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-installation-on-juniper-nfx-routers-9.png?alt=media)

    ​

### Uninstalling the ThousandEyes Juniper Virtual Appliance <a href="#uninstalling-the-thousandeyes-juniper-virtual-appliance" id="uninstalling-the-thousandeyes-juniper-virtual-appliance"></a>

To uninstall the ThousandEyes Virtual Appliance, use the following steps:

1.  1\.

    Connect to the JDM Connect to the JDM and enter configuration mode

    Entering configuration mode
2.  2\.

    Delete the ThousandEyes Virtual Appliance

    root\\# delete virtual-network-functions ThousandEyesVNF
3.  3\.

    Commit the changes to apply the configuration
4.  4\.

    Verify that the Virtual Appliance was deleted

    \## ID Name State Liveliness

### Managing the ThousandEyes Juniper Virtual Appliance <a href="#managing-the-thousandeyes-juniper-virtual-appliance" id="managing-the-thousandeyes-juniper-virtual-appliance"></a>

To connect to the VA, use the following command:

To restart to the VA, use the following command

To shut down to the VA, use the following command

To power up the VA, use the following command:

To check the VNF configuration, including the management IP:

Virtual Network Function Information

\-------------------------------------

IP Address: :192.168.1.102

Maximum Memory::2097152 KiB

vda\\| /var/third-party/images/thousandeyes-va-64-16.04.juniper-ch1.qcow2
