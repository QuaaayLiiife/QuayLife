# Installing Enterprise Agents in Proxy Environments

Some organizations' security policies require web communication (HTTP, HTTPS and FTP) from internal networks to the Internet be sent through a proxy server, in order to inspect and control the communication. Installation of an Enterprise Agent requires varying degrees of internet access, depending on the type of Enterprise Agent being installed. Additional or different installation steps may be required to install an Enterprise Agent when a proxy server is required for internet access.

Proxy servers have two principle characteristics which govern the way clients are configured:

* **Explicit or transparent** Proxy servers which require each client to be configured with the proxy's IP address (or hostname) and port number, and (optionally) user credentials, are called explicit proxies. Proxies which do not require clients to be configured with proxy information are called transparent proxies.
* **SSL decrypting or non-SSL decrypting** Proxy servers which perform SSL/TLS decryption require each client to be configured with the proxy's CA certificate (sometimes called a signing certificate or root certificate). Non-SSL decrypting proxies do not require clients to be configured with a CA certificate.

The figure below indicates the required configuration information for each of the four combinations of proxy type:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-933bb2cf78953bf83d31a10f86988ebb27d79b8a%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agents-in-proxy-environments-1.png?alt=media)

For proxies that are transparent and non-SSL decrypting, no additional configuration is required to perform the Enterprise Agent installation. Follow the installation instructions for your type of Enterprise Agent installation without a proxy.

The remaining three configurations of proxy are referred to in the remainder of this document with the following letters :

* **A:** Explicit, SSL decrypting proxy configuration
* **B:** Explicit, non-SSL decrypting proxy configuration
* **C:** Transparent, SSL decrypting proxy configuration

Consult with your proxy or network administrator to determine which type of proxy you have, and obtain all required information before proceeding.

### Types of Agent Deployment <a href="#types-of-agent-deployment" id="types-of-agent-deployment"></a>

* Deploying a Linux package agent

### Deploying a Linux Package Agent <a href="#deploying-a-linux-package-agent" id="deploying-a-linux-package-agent"></a>

Deploying a Linux package Agent is performed by downloading and running the install\_thousandeyes.sh shell script. The instructions for downloading and running the script are found by going to the **+ Add New Agent** form of the

[Enterprise Agents](https://app.thousandeyes.com/settings/agents/enterprise)

page, and selecting "Linux Package" for the **Package Type**, then clicking the **Show Advanced Options** link. The instructions are reproduced below:

curl -Os https://downloads.thousandeyes.com/agent/install\_thousandeyes.sh

chmod +x install\_thousandeyes.sh

sudo ./install\_thousandeyes.sh -b \<ACCOUNT-TOKEN>

In the first line, the curl command is used to download the install\_thousandeyes.sh file. The curl command may require additional flags to use the proxy.

In the third line, the install\_thousandeyes.sh script is executed. The script runs the Linux system's package management tool (if Ubuntu, the APT package manager; if Red Hat/CentOS/Oracle Linux, the YUM package manager) to download and install the Enterprise Agent software packages. To download and install the Agent through the proxy, the APT or YUM configuration file must be edited to include proxy information. Then the script configures the installed Agent. The script may require additional command line flags to use the proxy.

The following configuration steps may be required:

1.  1\.

    Install the proxy server's CA certificate
2.  2\.

    Configure the system package manager to use the proxy server
3.  3\.

    Run the **curl** command with modified flags
4.  4\.

    Run the **install\_thousandeyes.sh** script with modified flags

For proxy configuration A, B, or C, use the following table of steps:

**1. Install the proxy server's CA certificate**

**IMPORTANT:** Only install the CA certificate into the system CA certificate store. Do not perform the BrowserBot CA certificate installation, as the BrowserBot package is not yet installed.

**2. Configure the package manager to use the proxy server**

The install\_thousandeyes.sh script runs the system's package manager (APT or YUM) to download and install Agent packages. Additionally, the package manager will be used to automatically update the Agent packages and perform essential operating system updates. The procedure to configure the system package manager to use the proxy server is provided in the article

[Configuring an Enterprise Agent to use a proxy server](https://docs.thousandeyes.com/product-documentation/enterprise-agents/configuring-an-enterprise-agent-to-use-a-proxy-server)

. Select either the

[Ubuntu](https://docs.thousandeyes.com/product-documentation/enterprise-agents/configuring-an-enterprise-agent-to-use-a-proxy-server#configuring-proxy-settings-for-the-apt-package-manager-on-ubuntu)

or

[RHEL/CentOS/Oracle Linux](https://docs.thousandeyes.com/product-documentation/enterprise-agents/configuring-an-enterprise-agent-to-use-a-proxy-server#configuring-proxy-settings-for-the-yum-package-manager-on-rhel-centos-oracle-linux)

section.

The proxy used by the package manager need not be the same proxy used for the main Agent processes. Alternatively, if all needed repositories are mirrored on the internal network, or if communication to standard repositories on the Internet is permitted without a proxy, then this step can be skipped.

**3. Run the curl command with modified flags**

Modify the curl command to use flags for the proxy name or IP address and port number, and optionally a username and password:

\-x \<PROXY IP ADDRESS or HOSTNAME>:\<PROXY PORT> \\

\-U \<USERNAME>:\<PASSWORD> \\

\-Os https://downloads.thousandeyes.com/agent/install\_thousandeyes.sh

Depending on the characters used in the username and password, the `<USERNAME>:<PASSWORD>` string may need to be enclosed in double-quotes to avoid being interpreted by the shell.

**4. Run the install\_thousandeyes.sh script with modified flags**

Run the chmod command to make the script executable. Then, with the proxy name or IP address and port number, and optionally a username and password, modify the script command's flags:

chmod +x install\_thousandeyes.sh

sudo ./install\_thousandeyes.sh \\

\-P \<PROXY IP ADDRESS or HOSTNAME>:\<PROXY PORT> \\

The script will install the Enterprise Agent and the optional BrowserBot component. Omit the -b flag if BrowserBot is not required. The script will also configure the /etc/te-agent.cfg file with the proxy information provided by the command's flags.

Alternatively, if the Enterprise Agent will use a PAC file to select its proxy, then modify the script command for the PAC file:

chmod +x install\_thousandeyes.sh

sudo ./install\_thousandeyes.sh \\

To see all the supported command line flags of the script, use the --help flag:

./install\_thousandeyes.sh --help

**NOTE:** Authentication to the proxy is performed via the HTTP Basic authentication mechanism, including CONNECT method requests for subsequent HTTPS-based requests. Basic authentication credentials are sent in clear text, encoded in Base64. Organizations which do not allow any credentials to be transmitted on a network in clear text should consider alternatives to credential-based authentication to the proxy, such as configuring the proxy to allow-list Enterprise Agents via their IP addresses.

Deploying a Docker Enterprise Agent is performed by running a series of docker commands on the Docker host. The commands are created by going to the **+ Add New Agent** form of the

[Enterprise Agents](https://app.thousandeyes.com/settings/agents/enterprise)

page, and selecting "Docker" for the **Package Type**, then filling out the form.

The following configuration steps may be required:

1.  1\.

    Install proxy server's CA certificate on the Docker host
2.  2\.

    Configure Docker to use the proxy server

    * Ubuntu 16.04 / RHEL 7 / CentOS 7 or
3.  3\.

    Create Enterprise Agent Docker container with proxy configuration
4.  4\.

    Install proxy server's CA certificate into the Enterprise Agent container
5.  5\.

    Configure the container package manager to use the proxy server

For proxy configuration A, B or C use the following table of steps:

#### 1. Install proxy server's CA certificate on the Docker host <a href="#1.-install-proxy-servers-ca-certificate-on-the-docker-host" id="1.-install-proxy-servers-ca-certificate-on-the-docker-host"></a>

For other Linux distributions or non-Linux Docker hosts, consult your operating system documentation for more information on adding CA certificates to your system's certificate store, or contact the ThousandEyes Customer Engineering team.

**IMPORTANT:** Only install the CA certificate into the system CA certificate store. Do not perform the BrowserBot CA certificate installation.

#### 2. Configure Docker to use the proxy server <a href="#2.-configure-docker-to-use-the-proxy-server" id="2.-configure-docker-to-use-the-proxy-server"></a>

This procedure configures the Docker commands to use the proxy server when communicating to servers on the internet.

**2.1 Ubuntu 16.04 / Red Hat Enterprise Linux 7 / CentOS 7 / Oracle Linux**

Create the /etc/systemd/system/docker.service.d directory:

sudo mkdir -p /etc/systemd/system/docker.service.d

Edit the file in which then Docker proxy configuration will be stored:

sudo nano /etc/systemd/system/docker.service.d/proxy.conf

Enter the following environment variable configuration, replacing the sample values shown below with your proxy configuration information:

Reload the systemd configuration:

sudo systemctl daemon-reload

Restart the Docker service (warning, this command restarts all running Docker containers):

sudo systemctl restart docker

Verify whether the newly configured environment variables HTTP\_PROXY and HTTPS\_PROXY have the correct values:

sudo systemctl show --property=Environment docker

Download the Docker image using the docker pull command:

docker pull thousandeyes/enterprise-agent

Edit the file in which the Docker proxy configuration will be stored:

sudo nano /etc/default/docker

Append the following content, replacing the sample values shown below with your proxy configuration information:

Restart the Docker service (NOTE: this command restarts all running Docker containers):

Download the Docker image using the docker pull command:

docker pull thousandeyes/enterprise-agent

#### 3. Create Enterprise Agent Docker container with proxy configuration <a href="#3.-create-enterprise-agent-docker-container-with-proxy-configuration" id="3.-create-enterprise-agent-docker-container-with-proxy-configuration"></a>

Log in to the ThousandEyes web application and open the

[Enterprise Agents](https://app.thousandeyes.com/settings/agents/enterprise)

page. The commands to create the Enterprise Agent Docker container are produced by opening **+ Add New Agent** form and selecting "Docker" for the **Package Type**, then by completing the form. An example of the completed form is below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-265d9b0f53402bfd2931a832d0b15a52cf77eb98%2Fproduct-documentation\_enterprise-agents\_installing-enterprise-agents-in-proxy-environments-2.png?alt=media)
