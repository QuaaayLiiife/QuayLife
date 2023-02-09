# Installing Enterprise Agent on VirtualBox

This article describes how to set up the ThousandEyes Enterprise Agent using the Virtual Appliance OVA with VirtualBox. To download, VirtualBox visit

[https://www.virtualbox.org](https://www.virtualbox.org/)

.

See the installation guides for VirtualBox:

For your convenience, ThousandEyes provides an image of a virtual machine with the Enterprise Agent installed in OVA (Open Virtual Appliance) format, which is updated bi-weekly. Hence, we strongly recommend that you download a recent image for new Enterprise Agent installations. If your prefer more granular control of the your Enterprise Agent and the underlying operating system, we recommend you deploy the Enterprise Agent using the

[Linux Package method](https://docs.thousandeyes.com/product-documentation/enterprise-agents/enterprise-agent-deployment-using-linux-package-method)

.

To install the ThousandEyes Virtual Appliance, do the following:

1.  2\.

    Click **Add New Enterprise Agent**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d8b87e6d6578e0ab5cf6e7b25710fcb3de1c94ce%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-1.png?alt=media)
2.  3\.

    The **Add New Enterprise Agent** button reveals the installation options available for the Enterprise Agent. These instructions cover deployment using the OVA package. Select **Download - OVA** to get the latest version.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f81c34caefe2a28e2869f729fb53b0e313f496bb%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-2.png?alt=media)
3.  4\.

    Once the image is downloaded, open the VirtualBox application and click File > Import Appliance. The screenshot below is of VirtualBox version 5.2.20 r125813 (Qt5.6.3) on macOS Mojave. Depending on your operating system and version, what you see might have minor differences.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-704a862cb59e3398316a167d73561c4690dfccbc%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-3.png?alt=media)
4.  5\.

    Click **Browse** and select the downloaded virtual appliance image.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ca7b910079aa856b3f4e998ec54eebdb65bd1f99%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-4.png?alt=media)
5.  6\.

    Once the image is selected, click **Continue**.
6.  7\.

    The **Appliance settings** menu displays. Many options are preconfigured. However, the following options can be re-configured:

    The agent is designed to operate with the specifications listed in

    [Enterprise Agent Hardware Requirements](https://docs.thousandeyes.com/product-documentation/enterprise-agents/enterprise-agent-hardware-requirements)

    . If you choose settings higher than the recommended specifications, there are no additional benefits to the performance of the Enterprise Agent. However, performance will be degraded if you choose settings _below_ the recommendations. Once you've finished making changes, click **Import**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cfbf5e673f963703349d3f0658e09c812b14ba44%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-5.png?alt=media)
7.  8\.

    Wait for the appliance to be imported and visible in the VirtualBox Manager window. Once the import is complete (8), double-click the new machine to start.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0132a2ba062c5ba72ad8e179e1e2a5a4e73c510f%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-6.png?alt=media)
8.  9\.

    Once the machine boots up, a welcome screen displays the default values for the virtual appliance's IP address, username, and password. The virtual appliance's IP address is obtained via DHCP by default. If you are not using DHCP, you can configure a static IP by pressing **N** and following the interactive setup wizard. The available network configuration options are the following:

    To reset the virtual appliance password to the default value, press **R**. You can access the Web UI at

    https://\<Virtual Appliance IP address>

    . Access can be upgraded to HTTPS by following the steps mentioned

    [here](https://docs.thousandeyes.com/product-documentation/enterprise-agents/secure-access-to-thousandeyes-appliances)

    .

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-594c109719ab13d2e743ab424ae1f5130b90cca3%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-7.png?alt=media)
9.  10\.

    To open the web UI, open a web browser and enter the URL displayed on the welcome screen. Once you are at the URL, enter the default username and password. Then click **Login**. You will be prompted to change the default password. Enter the current and new passwords, then click **Change Password**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1f2da9aef0048453d9ee7c5dbc2fdb8a79d4ed06%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-8.png?alt=media)

1.  1\.

    Obtain the account group token as guided

    [here](https://docs.thousandeyes.com/product-documentation/enterprise-agents/where-can-i-get-the-account-group-token)

    . Navigate to the **Agent** tab in the web UI. Enter the account group token in the **Account Group Token** field; then click **Save Changes**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ae37635c3f3cce5d5670d49a3051b9cd4f929c06%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-9.png?alt=media)

1.  1\.

    The browser is now redirected to the **Review** page. Click **Complete** to finish setup.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2cc24c3216253a3847a07e97e15c86bdf87db4f9%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-10.png?alt=media)

1.  1\.

    If the **Review** page shows all checks green as in the screenshot above, your Enterprise Agent is now ready to run tests. The newly added Enterprise Agent will appear in the Settings > Enterprise Agents window, as seen below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0cf662204dfb1c2a8ef14f695261b4f146c01032%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agent-on-virtualbox-11.png?alt=media)

*   If your VM displays just a black screen, virtualization might be disabled or not available. On windows, you can confirm this using

    [these instructions](https://www.shaileshjha.com/how-to-find-out-if-intel-vt-x-or-amd-v-virtualization-technology-is-supported-in-windows-10-windows-8-windows-vista-or-windows-7-machine/)

    ​
*   If the path visualization appears broken or incomplete, this might be due to NAT. For a detailed explanation of this case, see

    [this article](https://docs.thousandeyes.com/product-documentation/advanced-troubleshooting/virtual-machine-with-nat-breaks-path-visualization)

    .
