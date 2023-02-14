# Discovering Device-Layer Devices

ThousandEyes Device Layer requires either SNMP version 2c or SNMP version 3. Device Layer retrieves the same data regardless of version SNMPv2c or SNMPv3, so you can configure either of the two versions. SNMPv3 provides better authentication, and data encryption in transfer.

Device Layer requires read-only access to the SNMP information. We recommend creating new read-only credentials for the Enterprise Agents, but existing read-only credentials can also be used.

Before the initial device discovery, perform the following steps:

1.  1\.

    Verify that each device will answer SNMP queries.
2. 2\.
   * the version of SNMP enabled
   * the community string (SNMPv2c) or authentication and privacy settings
3.  3\.

    Ensure that SNMP queries are allowed from the Enterprise Agent IP addresses to each device.

    Your target or other network devices (firewalls and other security devices) may restrict SNMP queries from Enterprise Agents to your target network devices using access control lists (ACLs). If so, add the Enterprise Agents' IP addresses to the ACLs. Allow SNMP queries destined to port 161/UDP.

ThousandEyes supports the following MIBs:

### Configuring Device Credentials <a href="#configuring-device-credentials" id="configuring-device-credentials"></a>

Device Layer requires your devices' SNMP credentials to discover the devices. In the ThousandEyes platform, go to **Devices > Device Settings > Device Credentials** tab. Click **Add New Credentials** to add a new set of credentials.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9c70acb61d87c40b0a4e5130ed87b658a5cb07c6%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-2.png?alt=media)

Give the credentials a meaningful name and select the SNMP version.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6c302092a36d6ad2261c483bc1676292d8f27ae8%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-3.png?alt=media)

SNMPv2 credentials consist of a single community string, which serves as a plain-text password.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8148f61bec98cf193bb031806a9d5b7f6094142b%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-4.png?alt=media)

* Authentication Protocol and Key (optional)
* Privacy Protocol and Key (optional; only if using an Authentication Protocol)

Click the **Add New Credentials** button to save the changes. If you have gathered different sets of credentials for different network devices, repeat the process for each set of credentials you have gathered.

With at least one device credential configured, you can configure one or more device discoveries in the **Devices > Device Settings > Device Discovery** tab. Device discovery can be performed manually, or can be scheduled at regular intervals ranging from 5 minutes to 24 hours.

ThousandEyes only allows valid IPV4 addresses in device discovery targets for SNMP monitoring.

Device discovery will poll targets specified in the discovery configuration. Polled devices may report interfaces on additional networks not specified in the targets. The Enterprise Agent can perform discovery on any additional networks, and polls discovered devices for further additional networks. This recursive process will continue until no new networks are found. In this way, the maximum number of pollable devices across all networks can be discovered without needing to manually configure polling for all devices. You can control the depth of the recursion in order to reduce the time or network traffic levels of the discovery process.

Additionally, you can control the discovery of devices through the use of allow lists and deny lists, which apply to the configured targets and to any networks discovered. If the lists overlap, deny lists take priority over allow lists.

To start a one-time device discovery, go to **Devices > Device Settings > Devices** tab and click **Find New Devices**. A discovery configuration form appears.

On the **Basic Configuration** tab of the form, configure the following settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f8dba32982a49e7229d158c02b6b104006ca2cff%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-5.png?alt=media)

* **Targets**: Specify which devices the Enterprise Agent should attempt to discover. Enter the hostname, IP address, IP address range (e.g., 192.168.1.1-192.168.1.10) or subnet (CIDR notation; e.g., 192.168.1.0/24).
* **Monitoring Agent**: Select an Enterprise Agent or an Enterprise Agent cluster to perform the discovery. Note the following:
  * If you select an Enterprise Agent cluster as the **Monitoring Agent**, as with all other testing performed by clusters, device-layer testing is performed by a single member of the cluster. The member is selected by the cluster load-balancing algorithm. If the agent performing the device-layer testing is removed from the cluster, device-layer testing is reassigned to another cluster member.
  * If an individual Enterprise Agent that is already performing device-layer testing is moved into an existing cluster, the device-layer view data collected before that agent joined the cluster will be no longer available. Device-layer data found on the Path Visualization view will continue to be available.
*   **Credentials**: Select all the credentials used by devices in the **Targets** field. These are the credentials that you entered in the

    [Configuring Device Credentials](broken-reference)

    step.
*   **Save as scheduled discovery**: If checked, the following additional fields appear to allow saving the discovery for automatic running:

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-daa39e6a9c99afeeb6038483c9fe11a3be04e43a%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-6.png?alt=media)

    ​
* **Discovery Name**: The name of the saved discovery configuration, which will be listed on the **Device Discoveries** tab.
* **Interval**: The time interval between automatic runs of this discovery.
* **Notification Rules**: The names of device notifications assigned to this discovery.

On the **Advanced Settings** tab of the form, configure the following settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-152afefaeecca3b76fe44d5fc28aacc5b17c16a7%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-7.png?alt=media)

* **Whitelist**: Specify devices within the **Targets** setting and from discovery which the Enterprise Agent should attempt to poll. Enter the IP address, IP address range (e.g., 192.168.1.1-192.168.1.10) or subnet (CIDR notation; e.g., 192.168.1.0/24). Hostnames are not permitted.
* **Blacklist**: Specify devices within the **Targets** setting and from discovery which the Enterprise Agent should not attempt to discover. Enter the IP address, IP address range (e.g., 192.168.1.1-192.168.1.10) or subnet (CIDR notation; e.g., 192.168.1.0/24). Hostnames are not permitted. If the lists overlap, deny lists take priority over allow lists.
* **Maximum Hops**: Limit the number of additional discovery attempts to perform, based on information returned by the discovered devices. The default is 0, which results in polling only the devices in the **Targets** field (no additional discovery attempts).
* **Connection Attempts**: Set the number of connection attempts per device. Heavily utilized devices or saturated networks may require multiple SNMP connection attempts per device.
* **Connection Timeout**: Set the timeout on each connection attempt.
* **Discovery Timeout**: Set the total time allowed for discovery. When the **Maximum Hops** setting is greater than 0, this setting can be useful to limit the discovery if discovered devices return large numbers of additional targets.
* **Query Mode**: Select **Fast** or **Compatible**.

To start a scheduled device discovery, go to **Devices > Device Settings > Device Discoveries** tab and click **Schedule Discovery**. A discovery configuration form appears.

On the **Basic Configuration** tab of the form, configure the following settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-94e8d0c77bbe0fdd3b4d82e9adc75e32f79f75c5%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-8.png?alt=media)

* **Discovery Name**: A name for this discovery configuration.
* **Targets**: Specify which devices the Enterprise Agent should attempt to discover. Enter the hostname, IP address, IP address range (e.g., 192.168.1.1-192.168.1.10) or subnet (CIDR notation; e.g., 192.168.1.0/24).
*   **Credentials**: Select all the credentials used by devices in the **Targets** field. These are the credentials that you entered in the

    [Configuring Device Credentials](broken-reference)

    step.
* **Monitoring Agent**: Select the monitoring agent that will perform the device discovery. This can be an Enterprise Agent or an Enterprise Agent cluster.
* **Interval**: Specify the frequency at which the discovery will be performed.
* **Notification Rules**: Select one or more Device Layer Notification Rules, in order to be notified when discovery produces new information, such as discovery of a new device or new interface on an existing device, or if an existing device is no longer contactable.

On the Advanced Settings tab of the form, configure the following settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-307c7cd8bf948c6925e1469b22a265a8787caf13%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-9.png?alt=media)

* **Whitelist**: Specify devices within the **Targets** setting and from discovery which the Enterprise Agent should attempt to poll. Enter the IP address, IP address range (e.g., 192.168.1.1-192.168.1.10) or subnet (CIDR notation; e.g., 192.168.1.0/24). Hostnames are not permitted.
* **Blacklist**: Specify devices within the **Targets** setting and from discovery which the Enterprise Agent should not attempt to discover. Enter the IP address, IP address range (e.g., 192.168.1.1-192.168.1.10) or subnet (CIDR notation; e.g., 192.168.1.0/24). Hostnames are not permitted. If the lists overlap, deny lists take priority over allow lists.
* **Maximum Hops**: Limit the number of additional discovery attempts to perform, based on information returned by the discovered devices. The default is 0, which results in polling only the devices in the **Targets** field (no additional discovery attempts).
* **Connection Attempts**: Set the number of connection attempts per device. Heavily utilized devices or saturated networks may require multiple SNMP connection attempts per device.
* **Connection Timeout**: Set the timeout on each connection attempt.
* **Discovery Timeout**: Set the total time allowed for discovery. When the **Maximum Hops** setting is greater than 0, this setting can be useful to limit the discovery if discovered devices return large numbers of additional targets.
* **Query Mode**: Select **Fast** or **Compatible**.
