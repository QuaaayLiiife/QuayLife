# Device Discovery Results

When

[device discovery](broken-reference)

has completed, new devices are displayed in **Devices > Device Settings > Devices** tab, at the top of the list. Additionally, the count of new devices is displayed to the left of the **Find New Devices** button.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e250303b27233c082b535b33dfbbeab469a7ef56%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-10.png?alt=media)

The list of devices includes the following for each row:

* **Name**: The SNMP name of the device. The **Name** field is populated from the discovered device's SNMP name, but can be changed.
* **Type**: The device type: firewall, load balancer, router, switch, or wireless access point. If the discovery process has not completed, this column may display **NEW** or **PENDING**.
* **Monitoring Agent**: The Enterprise Agent that queries this device.
* **Last Contact**: A green or red square showing a basic up or down status for the discovered device, and the time since the Enterprise Agent that is monitoring the device last tried to check in with the device.

To view the details of a device, click its row.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7426890598c0826069de4fdcfbb9610e7b5932bc%2Fproduct-documentation\_device-layer\_discovering-device-layer-devices-11.png?alt=media)

* **Name**: The SNMP name of the device. The **Name** field is populated from the discovered device's SNMP name, but can be changed.
* **Type**: The type of network device. The **Type** field is populated from the discovered device's SNMP device type, but can be changed. This setting controls the device's icon in the **Topology** view, but does not affect data collection.
* **IP / Hostname**: The IP address or hostname of the device. The **IP / Hostname** field is populated from the discovered device's SNMP device type, but can be changed to query the device on a different IP address.
* **Monitoring Agent**: Data from a discovered device is collected by a single Enterprise Agent. If a network device is discovered by multiple Enterprise Agents, use this setting to select which Enterprise Agent queries the device.
* **Monitored Interfaces**: The discovered network interfaces belonging to this device. All of a devices’s discoverable network interfaces are listed, but not monitored by default. Select the interfaces you would like to monitor. Keep in mind that a single agent can monitor a maximum of 20,000 interfaces. Discovery is still performed using only the interface specified in the **IP / Hostname** field.
* **Interval**: The frequency with which queries are sent to the device. The interval cannot be changed.
* **Credentials**: The credential that is used to poll this device. The credential can be changed.
* **Alert** **Rules**: Select the alert rules you want to use for device events.
* **Notification Rules**: Select the notification rules you want to use for device events.
* **Discovery Information**: The discovery configuration, monitoring agent, and credentials used to discover this device. You can click the discovery name to view the saved discovery configuration.
* **General Information**: The System Name, Vendor, Platform, and Description fields obtained from the device through the discovery process.
* **Device Uptime**: The device is polled every 5 minutes. If the device can respond to any SNMP queries, the device is considered up. Hover over the timeline to see details.
* **Monitoring Support**: Displays whether interface enumeration, IP addresses enumeration, and topology discovery are supported for this device.
* **Stop Monitoring**: This button stops the agent from polling the device via SNMP. Once stopped, the **Test** button is replaced with a **Monitor Device** button, which restarts monitoring.
* **Cancel**: Use this button to cancel any changes you've made to this device's configuration.
* **Test**: If you make changes to the configuration, the **Test** button becomes clickable. Click **Test** to test the configuration.
* **Save**: Click **Save** to save any changes.

### Troubleshooting Device Discovery <a href="#troubleshooting-device-discovery" id="troubleshooting-device-discovery"></a>

If a device cannot be discovered, do the following:

1.  1\.

    Go to **Devices > Device Settings > Devices** tab and click **Find New Devices**.
2.  2\.

    In the **Targets** field, enter the IP address of the device you would like to discover.
3.  3\.

    Ensure the **Credentials** match those configured on the network device.
4.  4\.

    Ensure there is SNMP connectivity between the selected Enterprise Agent and the device (destination UDP port 161).
5.  5\.

    Leave the default values in place on the **Advanced Settings** tab.

If manual discovery fails, check the device's logs and the logs of any firewall or packet filter between the Enterprise Agent and the device. Look for logged drops of UDP port 161 traffic. Alternatively, perform packet captures on the device to verify that SNMP communication reaches the device.
