# Installing Enterprise Agents on Cisco Routers with vManage

This article covers the steps to install a ThousandEyes Enterprise Agent on Cisco routers running in SD-WAN mode that are managed by vManage. For more information about vManage, see the

[vManage Documentation](https://www.cisco.com/c/en/us/solutions/enterprise-networks/sd-wan/vmanage.html)

.

vEdge routers must be added to the vManage inventory list before continuing. For more information, see the

[vManage Documentation](https://sdwan-docs.cisco.com/Product\_Documentation/vManage\_Help/Release\_18.3/Configuration/Devices)

.

To review the supported Cisco routers and hardware requirements, see the

[Support Matrix](https://docs.thousandeyes.com/product-documentation/integration-guides/thousandeyes-cisco-integration#support-matrix)

.

1.  1\.

    Log into the vManage portal.
2.  2\.

    Navigate to **Maintenance > Software Repository**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-20e1caa2f22fa54568f04168ada7be4fb500a621%2Finstalling-enterprise-agents-on-cisco-routers\_1.png?alt=media)

    ​

#### Optional: Add the Virtual Image <a href="#optional-add-the-virtual-image" id="optional-add-the-virtual-image"></a>

If this is a first time installation, add the virtual image first. Otherwise, move on to the next section:

1.  1\.

    Navigate to **Virtual Images**.
2.  2\.

    Select **Upload Virtual Image > vManage**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-744c8c403a01d17f76cdddd864ae345d235c64d3%2Finstalling-enterprise-agents-on-cisco-routers\_2.png?alt=media)

    ​
3.  3\.

    Upload the ThousandEyes installation image .tar file as an Image Package:

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-85f177fc940dba9c1216348f0f8cf5d89048f7a4%2Finstalling-enterprise-agents-on-cisco-routers\_3.png?alt=media)

    ​

**Note:** Once the image is uploaded, the filename should be present in the **Virtual Image** list.

To confirm the virtual image is ready, click **Show Info** to review and verify the virtual image's vnfProperties:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-045bac4e48f8f744b278235982c52c12b9d28521%2Finstalling-enterprise-agents-on-cisco-routers\_4.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-09f50463ffeb487df3d5283b32ac2f1a28eacd09%2Finstalling-enterprise-agents-on-cisco-routers\_5.png?alt=media)

#### Create the Feature Template <a href="#create-the-feature-template" id="create-the-feature-template"></a>

To create a template for a specific device type:

1.  1\.

    Navigate to **Configuration > Templates**.
2.  2\.

    Select **Feature > Create Template > Add Template**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9622be58eb23bdecccc1915b10a1e3c0ae24fa9f%2Finstalling-enterprise-agents-on-cisco-routers\_6.png?alt=media)

    ​
3.  3\.

    Under **Select Device**, search for the device model (for example, ISR4431) that you wish to deploy an agent to. See the

    [Support Matrix](https://docs.thousandeyes.com/product-documentation/integration-guides/thousandeyes-cisco-integration#support-matrix)

    for compatible routers.
4.  4\.

    Select **ThousandEyes Agent** template from under **Other Templates**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5e339d678806e0885d5d5b685a1a63ffeb6c7609%2Finstalling-enterprise-agents-on-cisco-routers\_7.png?alt=media)

    ​
5.  5\.

    Specify the template name and description.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0c77143412cde68224095f4069cb5624def4a46f%2Finstalling-enterprise-agents-on-cisco-routers\_8.png?alt=media)

    ​
6.  6\.

    Under **Basic Configuration**, enter the relevant **Account Group Token**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4166813f92dbe3b0902985d3e2c6c123dab73d90%2Finstalling-enterprise-agents-on-cisco-routers\_9.png?alt=media)

    ​
7.  7\.

    **Optional:** SD-WAN mode offers the option to send agent traffic to pre-configured VPN tunnels, instead of following the default management route. Specify the service VPN template (either Default, Global, or Device Specific) to deploy the ThousandEyes agent within. This will allow you to configure tests that collect telemetry on the SD-WAN overlay and the applicable underlay path. For more information on the available VPN template configurations, see the

    [vManage Documentation](https://sdwan-docs.cisco.com/Product\_Documentation/vManage\_Help/Release\_18.4/Configuration/Templates/VPN)

    .

    **Note:** Ensure that the agent has network reachability from within the service VPN to the ThousandEyes cloud dashboard over the Internet.
8.  8\.

    Under **Advanced**, configure the **Name Server**, **Hostname**, and **Web Proxy**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e829bdb35f4b3279c6688d8c89a848beef6850cc%2Finstalling-enterprise-agents-on-cisco-routers\_10.png?alt=media)

    ​

    **Note:** This proxy configuration doesn't support any authentication methods. If you need to configure a proxy that requires basic or PAC authentication, you will need to use the CLI deployment option.
9.  9\.

    Click **Save** to save the template.

#### Attach the Feature Template to the Device Template. <a href="#attach-the-feature-template-to-the-device-template." id="attach-the-feature-template-to-the-device-template."></a>

1.  1\.

    Navigate to **Configuration > Template > Device**, then search for the device type (i.e. ISR4221x).
2.  2\.

    Click the three dots icon and select **Edit**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-496ac1270b4ba04dcdc9625135267063c2f34560%2Finstalling-enterprise-agents-on-cisco-routers\_12.png?alt=media)

    ​
3.  3\.

    Navigate to the **Additional Template**.
4.  4\.

    Open the **ThousandEyes Agent** drop-down menu, and select the template created in steps 2-9.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f689a2aea26af402bfa0f54c16554041a682da81%2Finstalling-enterprise-agents-on-cisco-routers\_13.png?alt=media)

    ​
5.  5\.

    Click **Update** to save the changes.

#### Attach the Device Template to a Device <a href="#attach-the-device-template-to-a-device" id="attach-the-device-template-to-a-device"></a>

1.  1\.

    Click the three dots icon and select **Attach Devices**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7f7dc5a0c6e98934edc6b6bf8a66fa41de91eef6%2Finstalling-enterprise-agents-on-cisco-routers\_14.png?alt=media)

    ​
2.  2\.

    Select the desired device/s from the **Available Devices** list, then click **Attach**.

    **Note:** The list will only contain vEdge devices that are the same model as the template.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0b64049e2647649b63c2556c83070534735c8252%2Finstalling-enterprise-agents-on-cisco-routers\_15.png?alt=media)

    ​

Once the template is attached to the desired devices, you can verify it from the **Running Configuration** view:

1.  1\.

    Navigate to **Configuration > Devices**.
2.  2\.

    Click the three dots icon beside the desired device, and select **Running Configuration**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9103fc3f33230c4f7ce90e9404252a3ccf8c3d27%2Finstalling-enterprise-agents-on-cisco-routers\_16.png?alt=media)

    ​

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f7b1a86f24f734571c6bb0fd682b020210937cf9%2Finstalling-enterprise-agents-on-cisco-routers\_17.png?alt=media)

    ​

Agents can be un-deployed by removing the ThousandEyes Agent feature template from the device template. However, vManage cannot disable the running Agents once they are deployed. You will need to use either the web app or the CLI for agent management. See

[Reconfiguring the Docker Container](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/cisco-devices/installing-enterprise-agents-on-cisco-routers#reconfigure-the-docker-container)

for CLI instructions.

### Frequently Asked Questions <a href="#frequently-asked-questions" id="frequently-asked-questions"></a>

**What is the expected NTP behavior for a Catalyst 8000 series deployed Enterprise agent?**

The enterprise agent on a Catalyst 8000 series switch uses the host system kernel clock. It also sends packets to **pool.ntp.org** to determine any clock offset. It does not try to adjust the host or container clock but will adjust measurement timestamps based on the clock offset.

**Can the default external NTP source (pool.ntp.org) be changed to a customer's internal NTP source?**

No. The agent uses **pool.ntp.org** to determine clock offset by default; this is currently not configurable.

**How do I connect to the agent shell for Cisco agents?**

To access the agent shell of a Cisco Enterprise Agent that is actively running, use the following command:

catalyst#app-hosting connect appid {application name} session

Once inside the agent shell, you can refer to the agent log for any further troubleshooting:

\# tail /var/log/agent/te-agent.log

If connection or DNS resolution errors are found in the log file, your agent cannot connect to the ThousandEyes platform. Check your app-vnic configuration and make sure the agent IP can reach the internet.

**Can I use ThousandEyes troubleshooting utilities?**
