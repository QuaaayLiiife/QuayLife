# Enterprise Agent Interface Selection

When a ThousandEyes Enterprise Agent has multiple network interfaces each with a unique IP address, or has a single interface with multiple IP addresses, the Interface Selection feature allows a test to use a specific interface or IP address. The test will use the assigned interface to perform all measurements, and set the source IP address of packets to the desired IP address. By providing test-level control of source IP addresses, Interface Selection allows customers to direct test traffic using policy-based routing or similar mechanisms, such as those found in SD-WAN environments.

Using Interface Selection and multiple tests, a customer can configure a single Enterprise Agent to monitor a given target via multiple paths. A common use case is monitoring a multi-homed site or enterprise. When an organization has more than one connection to the Internet, a single Enterprise Agent can run multiple tests, each assigned to a specific link. Links may be physical, or may be Virtual Private Network (VPN) links.

If SD-WAN technology is employed, a dedicated test and interface/address could be used to identify which path the SD-WAN currently uses. The Path Visualization will display hops specific to a path, whether overlay or underlay. Alerts may be constructed based on the IP addresses of hops in the the path.

Interface Selection is available for all test types except browser-based tests (Page Load and Transaction tests) and DNS layer tests. The Agents selectors for these test types will not display any additional interface information on an Enterprise Agent with multiple interfaces. This applies to all views of the test type, i.e. a Page Load test's HTTP Server view and Network layer views will not display the Interface Selection.

Depending on the current configuration of the system running your Enterprise Agent, configuring Interface Selection is done in up to three steps if adding additional physical or virtual network interfaces, or up to two steps if adding additional IP addresses to an existing interface:

1.  1\.

    Create the physical or virtual network interface adapter for the system (if using multiple interfaces; skipped if using one interface with multiple addresses)
2.  2\.

    Configure the interface with new IP information
3.  3\.

    Configure a test to use the network interface/IP address

To support Interface Selection with multiple interfaces, the system running an Enterprise Agent must either have multiple network interfaces already installed or the system must have one or more interfaces added. The process to add interfaces depends on the physical hardware, virtualization technology (if used), and operating system. Review the documentation for your hardware, virtualization technology and operating system to add new interfaces, if needed.

Skip this step if using Interface Selection with a single interface having multiple IP addresses.

#### 2) Interface configuration <a href="#2-interface-configuration" id="2-interface-configuration"></a>

Interface Selection supports multiple interfaces each with a single IP address, or a single interface with multiple IP addresses. ThousandEyes appliances provide configuration of IP information (IP address, netmask, default gateway, etc...) through the web-based administration. Other Agent installation types (Linux package, Docker) are configured according to the operating system used. Review the documentation for your operating system, and review the instructions for your installation type in the **Agent Configuration** section below.

Once an Enterprise Agent has multiple interfaces or IP addresses configured, tests can be configured to use a specific interface/address of that Agent. A test's **Agents** selector will display the Enterprise Agent with a triangle expander icon beside the Agent's name. Clicking the checkbox beside the Agent's name will make the radio buttons clickable, allowing selection of an interface/IP address.

The selector below displays an Enterprise Agent with two network interfaces, eth0 (IP address 10.100.10.108) and eth1 (IP address 10.100.10.73).

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-87a5f46cdfc46b271292fb9fb334cfde91278745%2Fenterprise-agent-interface-selection\_2.png?alt=media)

#### Multiple addresses on a single interface <a href="#multiple-addresses-on-a-single-interface" id="multiple-addresses-on-a-single-interface"></a>

The selector below displays an Enterprise Agent with one network interface, eth0, with two IP addresses 192.168.1.81 and 192.168.1.112.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b26f26e9f61b8a6207125dc0d92b85d3b1317316%2Fenterprise-agent-interface-selection\_3.png?alt=media)

The selector will also list a **Default interface selection** radio button, which will be selected by default. The default interface will be one of the interfaces listed below the **Default interface selection** radio button. If the system was originally configured with a single interface, then the default interface is usually the original interface. This option exists for users who may be unfamiliar with the Interface Selection feature, to allow them to select an interface that is likely to be sufficient for their needs.

The default interface is the interface associated with the system's default routing table:

default via 192.168.1.254 dev eth0 onlink

169.254.1.0/24 dev eth0 proto kernel scope link src 169.254.1.2

172.21.86.172/30 dev sb\_parent proto kernel scope link src 172.21.86.173

192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.83

The command `ip route show` displays the default interface of eth0/192.168.1.83, as shown in the previous image.

The sections below provide instructions to configure each type of Enterprise Agent installation: appliance (virtual or physical), Linux package, and Docker. Each section contain instructions for both the multiple interfaces and single interface/multiple addresses scenarios. Follow the instructions in the section which applies to your type of Enterprise Agent installation and interface/address scenario.

**NOTE:** An Enterprise Agent can only be configured with multiple interfaces or with a single interface having multiple IP addresses. An Enterprise Agent cannot be configured with both methods.

**NOTE:** Interface Selection is not supported on Enterprise Agent clusters.

**NOTE:** The ThousandEyes appliance is typically the easiest installation type to configure when using Interface Selection. Configuration of Linux package and Docker installation types has limitations, and all configuration of the interfaces and addresses is the responsibility of the customer. ThousandEyes recommends using an appliance installation if Interface Selection is required.

The ThousandEyes virtual appliance and physical appliance are configured through the appliance's web administration interface. Log into the web interface and select the appliance's Network tab to configure any additional interfaces or IP addresses. See the following articles for more information on accessing and navigating the web administration interface:

To configure multiple interfaces, first add a virtual network interface in the hypervisor software used to run the virtual appliance, or add a physical network interface. Consult your hypervisor's documentation for instructions on adding a virtual network interface (virtual appliance) or hardware documentation for instructions on adding a physical network interface (physical appliance).

When the appliance has been configured with an additional interface(s), log in to the appliance's web administration console. The **Network** tab displays the initial configuration field(s) for the additional interface(s) below the default interface.

In the configuration setting, select either **Using DHCP** or **Manually**, then configure the IP settings that appear. Note that **Physical Address** is not a configurable field.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1c3548af75677a211e47445f92a00e940ac22c67%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-interface-selection-1.png?alt=media)

Click **Save** at the bottom of the page to save the configuration.

**Multiple addresses on a single interface**

To configure multiple interfaces, login to the appliance's web administration console. The **Network** tab will display the **+ Add IP address** link below the default interface. In the image below, interface eth0 is available for configuration:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b34dbc0903748636096381170d01ced0154ea85e%2Fenterprise-agent-interface-selection\_4.png?alt=media)

Click the **+ Add IP address** link then configure the IP settings that appear. The **Name** field is a string without whitespace which can be used to identify the purpose of the interface, and will be displayed in the Agents selector of tests. For example, the string "SD-WAN\_IP" could be used to identify an IP address used in an SD-WAN overlay.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-da6c1b0597edcbfdd11381139d82522a9b762995%2Fenterprise-agent-interface-selection\_5.png?alt=media)

For supported versions of Ubuntu, Red Hat Enterprise Linux, CentOS and Oracle Linux, customers will need to perform the configuration tasks needed to create interfaces, and then configure the interfaces either statically or via DHCP. Additionally, creation of a new routing table may be required via the iproute2 package, or similar tool.

To configure multiple interfaces, first add a physical network interface, or virtual network interface in the hypervisor software used to run the appliance. Consult your hardware or hypervisor documentation for instructions on adding a network interface.

When the system has been configured with an additional interface(s), consult the documentation for your Linux distribution to add IP configuration manually to the interface, and create a routing table for the interface if needed. Configuring the interface via DHCP is not supported when an interface uses a dedicated routing table.

**Multiple addresses on a single interface**

To configure a single interface with multiple IP addresses, manually add the IP information to the interface. DHCP is not supported for multiple addresses on a single interface. An example set of commands is below for configuring eth0.

1.  1\.

    Add the new IP address to the running system

ip addr add 10.0.0.1/8 dev eth0 label eth0:1

1.  1\.

    Add to `/etc/network/interfaces` to persist across reboots

For the ThousandEyes Docker image, customers will need to perform the configuration tasks needed to create interfaces when invoking the `docker run` command, and then configure the interfaces either statically or via DHCP. Additionally, creation of a new routing table may be required via the iproute2 package, or similar tool. Consult the Docker documentation for further configuration details. The ThousandEyes Docker image is based on Ubuntu, so any configuration within the container follows the instructions above for Linux packages.

### Viewing selected interfaces <a href="#viewing-selected-interfaces" id="viewing-selected-interfaces"></a>

After configuring the Interface Selection feature, selected IP addresses will be displayed in the Path Visualization view. In other test views and parts of the app, the default interface will be displayed.

#### Interface Selection in the Path Visualization view <a href="#interface-selection-in-the-path-visualization-view" id="interface-selection-in-the-path-visualization-view"></a>

When a test uses an Agent's non-default interface, the Path Visualization view will display the selected interface used in the Agent's tooltip, under the **Interface Details**. Mouse over an Agent in the Path Visualization to display the tooltip:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1d5c993e70d5b878e841f1e916fbef53ef0cb645%2Fenterprise-agent-interface-selection\_6.png?alt=media)

In the image above, the IP address 10.100.10.73 from interface eth1 is used for the test.

#### Interface Selection in the Overview <a href="#interface-selection-in-the-overview" id="interface-selection-in-the-overview"></a>

In the Overview, the Table tab will display the default interface, and any public IP address (NAT IP address) associated with the default interface:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ff52b258356216d42ad372b50a989acb10d33b9e%2Fenterprise-agent-interface-selection\_7.png?alt=media)

In the image above, the IP address 10.100.10.108 from interface eth0 is displayed, although the test used eth1 (10.100.10.73).

#### Interface Selection in Agent Settings <a href="#interface-selection-in-agent-settings" id="interface-selection-in-agent-settings"></a>

In other views or areas of the app, the default interface's information will be displayed, such as the Agent's General Information section of the Agent Settings page:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ebd818153da4afcfcea106ec99f1d840988e1cc2%2Fenterprise-agent-interface-selection\_8.png?alt=media)

In the image above, the IP address 10.100.10.108 from the default interface, eth0, is displayed in the **Private IP Address** field. The default interface is always used to contact ThousandEyes for data upload and configuration downloads. Note that the public IP address (NAT IP address) is the address associated with the connections made to ThousandEyes from 10.100.10.108. The public IP address may be the same for traffic from the eth1 interface (10.100.10.73) to the internet, or the public IP address may be different if more than one NAT IP address is available, such as when a NAT address pool is configured on the NAT device, or if multiple paths to the Internet exist and traverse different NAT devices.

A test may display an error similar to the following:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-46fb0cf49f2ec5dec2340695b9263940e09c1a4b%2Fenterprise-agent-interface-selection\_9.png?alt=media)

The message "Cannot use the selected interface" appears in the Error Details column. Some reasons for this error:

1.  1\.

    The test uses Interface Selection with a specific (non-default) interface which becomes unavailable.
2.  2\.

    The test uses Interface Selection with a specific (non-default) IPv4 interface but the test's IPv6 **Policy** setting (on the Advanced Settings tab) is configured with "Force IPv6" or "Prefer IPv6" or "Agent's policy" where the policy is "Force IPv6" or "Prefer IPv6" and the test target is either an IPv6 IP address or a domain name that resolves to an IPv6 address.
3.  3\.

    The test uses Interface Selection with a specific (non-default) IPv6 interface but the test's IPv6 **Policy** setting (on the Advanced Settings tab) is configured with "IPv4 only" or "Agent's policy" where the policy is "IPv4 only" and the test target is either an IPv4 IP address or a domain name that resolves to an IPv4 address.
4.  4\.

    The message “Cannot use the selected interface” can occur in all scenarios, not only those where the user has manually selected a particular interface. You may also see it when an interface is automatically selected by the agent as well. The same troubleshooting steps are relevant for the error no matter how it occurs.
