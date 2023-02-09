# Installing Enterprise Agents on Cisco Routers with Docker

This article provides an overview of the steps to install a ThousandEyes Enterprise Agent on a supported Cisco router using Docker. The Docker agent is a signed ThousandEyes Docker image that can be quickly launched using Cisco application hosting.

To review the supported Cisco routers and hardware requirements, see the

[Support Matrix](https://docs.thousandeyes.com/product-documentation/integration-guides/thousandeyes-cisco-integration#support-matrix)

.

Both SD-WAN and Autonomous mode are supported.

Deploying an Enterprise Agent on a Cisco router requires the completion of three steps. These steps are detailed in the sections below:

1.  1\.

    Install the Enterprise Agent on the Cisco router, using one of three available methods (bootflash, direct, via local machine).
2.  2\.

    Configure the container's networking and account information.
3.  3\.

    Verify the agent is running.

For Cisco routers purchased before August 15th, 2021, the Docker image can be installed either directly from the ThousandEyes download servers, or by downloading the container image to a local machine and uploading it to the router via SCP, FTP, TFTP, or USB storage, depending on whether the router has direct Internet access or not.

Routers purchased after August 15th, 2021, can, in addition to the previous methods, install the Enterprise Agent via bootflash.

#### Install the Docker Image from Bootflash <a href="#install-the-docker-image-from-bootflash" id="install-the-docker-image-from-bootflash"></a>

If the router was purchased after August 15th, 2021, the router will have the ThousandEyes Enterprise Agent available in bootflash.

To verify if it is available, use the following command: `Dut1#dir bootflash:/apps`.

1.  1\.

    Run the following command to install via bootflash:

    \#app-hosting install appid package bootflash:apps/thousandeyes-enterprise-agent-4.2.2.cisco.tar

#### Install the Docker Image to the Router Directly <a href="#install-the-docker-image-to-the-router-directly" id="install-the-docker-image-to-the-router-directly"></a>

If the Cisco router has direct internet access, follow the steps below to install the Enterprise Agent:

1.  1\.

    Run the following command to install the image:

    catalyst#app-hosting install appid \<app-name> package https://downloads.thousandeyes.com/enterprise-agent/thousandeyes-enterprise-agent-4.2.2.cisco.tar
2.  2\.

    Your application should now be installed. You can check on it by running the following:

    catalyst#sh app-hosting list

    thousandeyes\_enterprise\_agent DEPLOYED

#### Install the Docker Image via a Local Machine <a href="#install-the-docker-image-via-a-local-machine" id="install-the-docker-image-via-a-local-machine"></a>

If the Cisco router does not have direct access to the Internet, follow the steps in the sections below to install the Enterprise Agent.

**Download the Docker Image to a Local Machine**

Download the Docker image from the ThousandEyes dashboard and copy it to your Cisco router using SCP, FTP, TFTP, or USB storage.

1.  1\.

    On your local machine, log into the ThousandEyes platform using a login belonging to the account group that will be associated with the appliance.
2.  2\.

    Navigate to **Cloud & Enterprise Agents > Agent Settings** and click **Add New Enterprise Agent**.
3.  3\.

    Download the .tar file with the ThousandEyes appliance for Catalyst 8000-series or ISR 4000-series routers.
4.  4\.

    Use SCP, FTP, TFTP, or USB storage to copy the signed Docker image to the router's flash: directory.
5.  5\.

    Run the following command:
6.  6\.

    Run a checksum (md5) command to verify that the package transfer was successful. The md5 output should match `571d0477f2d1517a9dc90c7ef15456b9`.

    catalyst#verify /md5 (flash:thousandeyes-enterprise-agent-4.2.2.cisco.tar) = 571d0477f2d1517a9dc90c7ef15456b9

**Install the Docker Image from a Local Machine**

1.  1\.

    Enable the IOx framework on the router. Enter one configuration command per line, and end with CNTL/Z:
2.  2\.

    Wait until all the services are running:

    catalyst#show iox-service

    IOx Infrastructure Summary:

    IOx service (CAF) : Running

    IOx service (HA) : Not Supported

    IOx service (IOxman) : Running

    IOx service (Sec storage) : Not Supported
3.  3\.

    Run the installation command, specifying your desired app name and the location of the image file you want to use. In this example, we use **thousandeyes\_enterprise\_agent**:

    catalyst#app-hosting install appid \<app-name> package flash:thousandeyes-enterprise-agent-4.2.2.cisco.tar
4.  4\.

    If the image is hosted on an HTTPS server, you can run the following command to download the image:

    catalyst#app-hosting install appid \<app-name> package https://downloads.thousandeyes.com/enterprise-agent/thousandeyes-enterprise-agent-4.2.2.cisco.tar
5.  5\.

    Your application should now be installed. You can check on it by running the following:

    catalyst#sh app-hosting list

    thousandeyes\_enterprise\_agent DEPLOYED

Docker supports both static IP address assignment and dynamic IP address assignment. You must configure a single virtual network interface card (vNIC) for the appliance using either a management interface or virtual port group interface.

There are two available configuration paths, detailed in the sections below:

#### Option One: VirtualPortGroup Interface <a href="#option-one-virtualportgroup-interface" id="option-one-virtualportgroup-interface"></a>

1.  1\.

    Configure the VirtualPortGroup interface with a private IP address and use as NAT inside:

    (config)interface VirtualPortGroup0

    (config)ip address 10.100.152.100 255.255.255.0
2.  2\.

    Configure NAT outside on the physical port interface:

    (config)interface GigabitEthernet0/0/3
3.  3\.

    (config)ip nat inside source list NAT interface GigabitEthernet0/0/3 overload

    (config)ip access-list extended NAT

    (config)10 permit ip 10.100.152.0 0.0.0.255 any
4.  4\.

    Configure the application, either with a static IP or with DHCP IP:

    a. Configuration with Static IP:

    Use a guest IP address to assign a static IP address. In this example, assign 10.100.152.120/24 from VirtualPortGroup 0 and use Google resolver:

    (config)#app-hosting appid c8200

    (config-app-hosting)#app-vnic gateway0 virtualportgroup 0 guest-interface 0

    (config-app-hosting-gateway0)#guest-ipaddress 10.100.152.120 netmask 255.255.255.0

    (config-app-hosting-gateway0)#app-default-gateway 10.100.152.100 guest-interface 0

    (config-app-hosting-docker)#name-server0 8.8.8.8

    Next, set up the required Docker run options to specify account token. If you want to specify a hostname other than the router's name, do this here as well:

    catalyst(config-app-hosting)#app-resource docker

    catalyst(config-app-hosting-docker)#prepend-pkg-opts

    catalyst(config-app-hosting-docker)#run-opts 1 "-e TEAGENT\_ACCOUNT\_TOKEN=\<Token>"

    catalyst(config-app-hosting-docker)#run-opts 2 "--hostname Cisco-Docker"

    catalyst(config-app-hosting)#start

    catalyst(config-app-hosting)#end

    b. Configuration with DHCP IP:

    Make sure the DHCP server is running on the VirtualPortGroup interface.

    (config)#app-hosting appid c8200

    (config-app-hosting)#app-vnic gateway0 virtualportgroup 0 guest-interface 0

    (config-app-hosting-docker)#name-server0 8.8.8.8

    Next, set up the required Docker run options to specify the account token same as the static IP assignment example above.
5.  5\.

    Exit three times to completely exit out of config mode.
6.  6\.

    Use **wr mem** to ensure that your configuration changes have persisted across reboots:

    Building configuration...

#### Option Two: Management Interface Configuration <a href="#option-two-management-interface-configuration" id="option-two-management-interface-configuration"></a>

1.  1\.

    Configure the management interface:

    interface GigabitEthernet0

    ip address 10.82.139.212 255.255.255.240
2.  2\.

    Configure the application, either with a static IP or with DHCP IP:

    a. **Configuration with Static IP**:

    1.  1\.

        Use a guest IP address to assign a static IP address. In this example, assign `10.82.139.211/24` from GigabitEthernet 0 and use the Google resolver:

        (config)#app-hosting appid c8200

        (config-app-hosting)#app-vnic management guest-interface 0

        (config-app-hosting-gateway0)#guest-ipaddress 10.82.139.211 netmask 255.255.255.0

        (config-app-hosting-gateway0)#app-default-gateway 10.82.139.212 guest-interface 0

        (config-app-hosting-docker)#name-server0 8.8.8.8
    2.  2\.

        Set up the required Docker run options to specify the account token. If you want to specify a hostname other than the router's name, do this here as well:

        catalyst(config-app-hosting)#app-resource docker

        catalyst(config-app-hosting-docker)#prepend-pkg-opts

        catalyst(config-app-hosting-docker)#run-opts 1 "-e TEAGENT\_ACCOUNT\_TOKEN=\<Token>"

        catalyst(config-app-hosting-docker)#run-opts 2 "--hostname Cisco-Docker"

        catalyst(config-app-hosting)#start

        catalyst(config-app-hosting)#end

    b. **Configuration with DHCP IP**:

    1.  1\.

        Make sure the DHCP server is running on the management interface:

        (config)#app-hosting appid c8200

        (config-app-hosting)#app-vnic management guest-interface 0

        (config-app-hosting-docker)#name-server0 8.8.8.8
    2.  2\.

        Set up the required Docker run options to specify the account token. If you want to specify a hostname other than the router's name, do this here as well:

        catalyst(config-app-hosting)#app-resource docker

        catalyst(config-app-hosting-docker)#prepend-pkg-opts

        catalyst(config-app-hosting-docker)#run-opts 1 "-e TEAGENT\_ACCOUNT\_TOKEN=\<Token>"

        catalyst(config-app-hosting-docker)#run-opts 2 "--hostname Cisco-Docker"

        catalyst(config-app-hosting)#start

        catalyst(config-app-hosting)#end
3.  3\.

    Exit three times to completely exit out of config mode.
4.  4\.

    Use **wr mem** to ensure that your configuration changes have persisted across reboots:

    Building configuration...

With the `(config-app-hosting)#start` command, the Docker container should have been started and should be running. You can verify this through the following options:

c8200# sh app-hosting list

thousandeyes\_enterprise\_agent RUNNING\`

Verify the Docker container’s details:

c8200#sh app-hosting detail appid c8200

Name : ThousandEyes Enterprise Agent

Path : bootflash:thousandeyes-enterprise-agent-4.2.2.cisco.tar

Activated profile name : custom

Platform resource profiles

Profile Name CPU(unit) Memory(MB) Disk(MB)

\--------------------------------------------------------------

\---------------------------------------------

serial/shell iox\_console\_shell serial0

serial/aux iox\_console\_aux serial1

serial/syslog iox\_syslog serial2

serial/trace iox\_trace serial3

\---------------------------------------

MAC address : 52:54:dd:e9:9e:9f

IPv4 address : 10.100.152.122

In the ThousandEyes platform, go to **Cloud & Enterprise Agents > Agent Settings** and verify the Docker container’s IP address.

### Modify the Docker Container <a href="#modify-the-docker-container" id="modify-the-docker-container"></a>

1.  1\.

    catalyst# app-hosting stop appid thousandeyes\_enterprise\_agent

    thousandeyes\_enterprise\_agent stopped successfully

    Current state is: STOPPED
2.  2\.

    De-activate the application:

    catalyst# app-hosting deactivate appid thousandeyes\_enterprise\_agent

    thousandeyes\_enterprise\_agent deactivated successfully

    Current state is: DEPLOYED
3.  3\.

    Modify the Docker options, and exit three times:

    catalyst(config)#app-hosting appid thousandeyes\_enterprise\_agent

    catalyst(config-app-hosting)#app-resource docker

    catalyst(config-app-hosting-docker)#prepend-pkg-opts

    catalyst(config-app-hosting-docker)#\<run-opts command>

    catalyst(config-app-hosting-docker)#exit

    catalyst(config-app-hosting)#exit
4.  4\.

    Reactivate the application, and confirm that it’s activated:

    catalyst# app-hosting activate appid thousandeyes\_enterprise\_agent

    thousandeyes\_enterprise\_agent activated successfully

    Current state is: ACTIVATED
5.  5\.

    Start the application, and confirm that it is running:

    catalyst# app-hosting start appid thousandeyes\_enterprise\_agent

    thousandeyes\_enterprise\_agent started successfully

    Current state is: RUNNING

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

**What are the default trusted default root certificates used by the Enterprise Agent Docker container when communicating with ThousandEyes services?**

* issuer=O = Cisco, CN = Cisco Licensing Root CA
* issuer=O = Cisco, CN = Cisco Basic Assurance Root CA 2099
* issuer=O = Cisco, CN = Cisco ECC Root CA
* issuer=O = Cisco Systems, CN = Cisco Root CA 2048
* issuer=O = Cisco, CN = Cisco Root CA 2099
* issuer=O = Cisco, CN = Cisco Root CA M1
* issuer=O = Cisco, CN = Cisco Root CA M2
* issuer=C = US, O = Cisco Systems, CN = Cisco RXC-R2
* issuer=C = US, O = Amazon, CN = Amazon Root CA 1
* issuer=C = US, O = Amazon, CN = Amazon Root CA 2
* issuer=C = US, O = Amazon, CN = Amazon Root CA 3
* issuer=C = US, O = Amazon, CN = Amazon Root CA 4
* issuer=C = NO, O = Buypass AS-983163327, CN = Buypass Class 2 Root CA
* issuer=C = US, O = DigiCert Inc, OU = www.digicert.com, CN = DigiCert Global Root CA
* issuer=C = US, O = Internet Security Research Group, CN = ISRG Root X1
* issuer=C = US, O = IdenTrust, CN = IdenTrust Commercial Root CA 1
* issuer=C = BM, O = QuoVadis Limited, CN = QuoVadis Root CA 2
* issuer=C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust ECC Certification Authority
* issuer=C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
* issuer=C = US, O = Google Trust Services LLC, CN = GTS Root R1
* issuer=C = US, O = Google Trust Services LLC, CN = GTS Root R2
* issuer=C = US, O = Google Trust Services LLC, CN = GTS Root R3
* issuer=C = US, O = Google Trust Services LLC, CN = GTS Root R4

**How do I install CA certificates on Cisco devices?**
