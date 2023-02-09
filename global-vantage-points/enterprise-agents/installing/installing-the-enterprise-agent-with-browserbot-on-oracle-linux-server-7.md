# Installing the Enterprise Agent with BrowserBot on Oracle Linux Server 7

By default, the Linux package installation of the Enterprise Agent on

[supported version of Oracle Linux operating system](https://docs.thousandeyes.com/product-documentation/enterprise-agents/supported-enterprise-agent-operating-systems)

will show a

[warning](https://docs.thousandeyes.com/product-documentation/enterprise-agents/install-the-enterprise-agent-with-browserbot-on-oracle-linux-server-7)

due to missing dependency packages for

[BrowserBot](https://docs.thousandeyes.com/product-documentation/enterprise-agents/what-is-browserbot)

component. The following step-by-step guide will enable the repository holding the Enterprise Agent dependency packages, before attempting to run the Enterprise Agent installation script.

All the commands below should be run as root. To reduce the content repetition, all "sudo" command prefixes have been removed and the whole guide assumes that you are running each command in a root shell.

To reach the root shell, use the following command:

The **expected output** is marked with **bold characters** on every sample command output below.

#### Step 1: Download the Oracle Linux Release 7 Update for x86 (64 bit) from the Oracle web site <a href="#step-1-download-the-oracle-linux-release-7-update-for-x86-64-bit-from-the-oracle-web-site" id="step-1-download-the-oracle-linux-release-7-update-for-x86-64-bit-from-the-oracle-web-site"></a>

#### Step 2: Install the Oracle Linux 7 Operating System <a href="#step-2-install-the-oracle-linux-7-operating-system" id="step-2-install-the-oracle-linux-7-operating-system"></a>

Proceed with a

[basic installation](https://oracle-base.com/articles/linux/oracle-linux-7-installation)

. In software selection, we recommend you proceed with the default **Minimal Install** under **Base Environment**.

#### Step 3: Enable the Oracle Optional repository (user either yum-config-manager or manually) <a href="#step-3-enable-the-oracle-optional-repository-user-either-yum-config-manager-or-manually" id="step-3-enable-the-oracle-optional-repository-user-either-yum-config-manager-or-manually"></a>

**3.1 With yum-config-manager**

\# yum install yum-utils -y

\# yum-config-manager --enable ol7\_optional\_latest

\# vi /etc/yum.repos.d/public-yum-ol7.repo

Use your preferred text editor to replace **enabled=0** with **enabled=1** on the section below, then save and exit the file.

name=Oracle Linux $releasever Optional Latest ($basearch)

baseurl=https://yum.oracle.com/repo/OracleLinux/OL7/optional/latest/$basearch/

gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle

#### Step 4: Install ThousandEyes Enterprise Agent <a href="#step-4-install-thousandeyes-enterprise-agent" id="step-4-install-thousandeyes-enterprise-agent"></a>

### Troubleshooting the Installation <a href="#troubleshooting-the-installation" id="troubleshooting-the-installation"></a>

The install\_thousandeyes.sh script, used with `-b` switch for installing BrowserBot, will display the warning:

Installing ThousandEyes' BrowserBot (Package required for Page Load and Transaction tests) \[ WARNING ]

(Failed installing ThousandEyes' BrowserBot)

Starting ThousandEyes' BrowserBot \[ WARNING ]

(Failed starting ThousandEyes' BrowserBot)

*   **Default ThousandEyes Linux Package Installation Log**

    Look for errors in the default installation log.

\# cat /tmp/install\_thousandeyes\*.log

ol7\_UEKR4/x86\_64 Latest Unbreakable Enterprise Kernel Release 4 for Oracle Linux 7Server (x86\_64) - enabled by default 110

ol7\_latest/x86\_64 Oracle Linux 7Server Latest (x86\_64) - required, enabled by default 12,501

ol7\_optional\_latest/x86\_64 Oracle Linux 7Server Optional Latest (x86\_64) - required, manually enabled at Step 3 9,608

thousandeyes ThousandEyes - required, enabled by the install\_thousandeyes.sh script 72
