# Installing and Removing ThousandEyes X Virtual Framebuffer on Enterprise Agents

With the release of `te-browserbot` 2.0, X Virtual Framebuffer is baked into the containerized runtime environment used by page load and transaction tests, so `te-xvfb` is no longer a requirement or suggested dependency of `te-browserbot`. This article is only applicable to agents running `te-browserbot` version 1.

For your convenience, ThousandEyes provides a wrapper of the X Virtual Framebuffer (Xvfb) installation package for installation on ThousandEyes Enterprise Agents. This wrapper is distributed as a Linux package called te-xvfb, and is included with all Enterprise Agent installations by default.

This article describes when you might need te-xvfb, and how to opt in or out of having it installed on ThousandEyes Enterprise Agents.

_"Xvfb is an X server that can run on machines with no display hardware and no physical input devices. It emulates a dumb framebuffer using virtual memory"_. You can read more about X Virtual Framebuffer

[here](https://www.x.org/releases/X11R7.6/doc/man/man1/Xvfb.1.xhtml)

.

### Do I Need to Install Xvfb? <a href="#do-i-need-to-install-xvfb" id="do-i-need-to-install-xvfb"></a>

Xvfb is not required for most browser-based test configurations, but there are notable exceptions.

If you are using Kerberos authentication or

[Proxy Auto-Configuration (PAC)](https://docs.thousandeyes.com/product-documentation/enterprise-agents/configuring-an-enterprise-agent-to-use-a-proxy-server)

for page load or transaction browser-based tests, you must install the ThousandEyes X Virtual Framebuffer on your Enterprise Agents.

When a browser-based test requiring Xvfb runs on an agent without Xvfb, an "X11 Service is not running" error is visible in the test's views.

### Installing Enterprise Agents with X Virtual Framebuffer <a href="#installing-enterprise-agents-with-x-virtual-framebuffer" id="installing-enterprise-agents-with-x-virtual-framebuffer"></a>

Installing an Enterprise Agent with Xvfb requires no additional effort:

* Linux package agents will come installed with te-xvfb unless the `-W` flag is passed to the `install_thousandeyes.sh` script
* Appliance (e.g. TEVA, TEPA, HyperV, etc.) images include te-xvfb.
* Docker images include te-xvfb.

### Installing Enterprise Agents without X Virtual Framebuffer <a href="#installing-enterprise-agents-without-x-virtual-framebuffer" id="installing-enterprise-agents-without-x-virtual-framebuffer"></a>

#### Linux Package Installation <a href="#linux-package-installation" id="linux-package-installation"></a>

Copy and run the following commands:

curl -Os https://downloads.thousandeyes.com/agent/install\_thousandeyes.sh

chmod +x install\_thousandeyes.sh

sudo ./install\_thousandeyes.sh -W -b \[ACCOUNT GROUP TOKEN]

1.  1\.

    Install the appliance as normal.
2.  3\.

    Run the following command:

    apt-get remove --purge te-xvfb

ThousandEyes does not distribute a Docker image that excludes Xvfb. To exclude Xvfb from a Docker agent installation, you must build a custom Docker image based on the standard ThousandEyes image:

1.  1\.

    Create a Dockerfile that conforms to the following template:

    FROM thousandeyes/enterprise-agent:latest

    RUN rm -rf /etc/service/te-xvfb
2.  2\.

    Build and push your custom Docker image.
3.  3\.

    Deploy a Docker agent using your customer Docker image in place of `thousandeyes/enterprise-agent`.

### Removing X Virtual Framebuffer from Existing ThousandEyes Agents <a href="#removing-x-virtual-framebuffer-from-existing-thousandeyes-agents" id="removing-x-virtual-framebuffer-from-existing-thousandeyes-agents"></a>

Once your agent has upgraded to a version of te-browserbot that no longer depends on te-xvfb (1.146 or greater), take the following installation-specific steps:

**Distributions Using `apt` (e.g. Ubuntu)**

Run the following command:

apt-get remove --purge te-xvfb

**Distributions Using `yum` (e.g. CentOS and RHEL)**

Run the following command:

1.  2\.

    Run the following command:

    apt-get remove --purge te-xvfb

You can remove X Virtual Framebuffer, but its removal will not persist across container restarts. We recommend re-installing the agent using a custom Docker image, as described above.

### Troubleshooting "X11 Service is not running" <a href="#troubleshooting-x11-service-is-not-running" id="troubleshooting-x11-service-is-not-running"></a>

If you encounter this error message, you can confirm that Xvfb is installed and running by checking its status:

#### Linux Package and Appliance Installation Types <a href="#linux-package-and-appliance-installation-types" id="linux-package-and-appliance-installation-types"></a>

systemctl status te-browserbot-xvfb
