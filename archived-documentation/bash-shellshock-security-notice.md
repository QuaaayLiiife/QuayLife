# Bash (ShellShock) Security Notice

On September 24, 2014, a critical vulnerability in the Bash shell (shipped with many Linux configurations) was documented in the National Vulnerability Database as CVE-2014-6271. This notification can be found on the NIST site at

[this link](http://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-6271)

.

ThousandEyes Enterprise Agents use Linux-based operating systems to run ThousandEyes Agent software, either by deploying the Ubuntu-based Virtual Appliance (“VA”, “VAs”), or installing the Agent package on a supported Linux operating system. Since both configurations leverage Linux, the Bash shell vulnerabilities collectively known as ShellShock (CVE-2014-6271, CVE-2014-7169, CVE-2014-7186, CVE-2014-7187) may be applicable to the platform running your Enterprise Agent:

_NOTE: As of September 24th, 2014, newly downloaded VAs have been patched for this vulnerability. Please see the section Identification of vulnerable systems for more information._

### Identification of Vulnerable Systems <a href="#identification-of-vulnerable-systems" id="identification-of-vulnerable-systems"></a>

Virtual Appliances downloaded from the ThousandEyes web site on or after September 24th, 2014 ,have been patched and are not vulnerable to this issue. Since ThousandEyes VAs are configured to download and apply security updates automatically, all Internet-connected VAs will have performed the update at this time.

To determine whether your Enterprise Agent’s platform is vulnerable, access your VA's command line using Secure Shell (SSH), and run the test command identified in the article above. We’ve excerpted the line below for your convenience.

#### ShellShock Vulnerability Test Command <a href="#shellshock-vulnerability-test-command" id="shellshock-vulnerability-test-command"></a>

$ env x='() { :;}; echo vulnerable' bash -c "echo this is a test"

#### Expected Vulnerable Response Signature <a href="#expected-vulnerable-response-signature" id="expected-vulnerable-response-signature"></a>

$ env x='() { :;}; echo vulnerable' bash -c "echo this is a test"

#### Expected Patched Response Signature (Ubuntu/Debian): <a href="#expected-patched-response-signature-ubuntu-debian" id="expected-patched-response-signature-ubuntu-debian"></a>

$ env x='() { :;}; echo vulnerable' bash -c "echo this is a test"

bash: warning: x: ignoring function definition attempt

bash: error importing function definition for 'x'

#### Expected Patched Response Signature (RedHat/CentOS): <a href="#expected-patched-response-signature-redhat-centos" id="expected-patched-response-signature-redhat-centos"></a>

$ env x='() { :;}; echo vulnerable' bash -c "echo this is a test"

Since SSH access is tightly controlled on ThousandEyes VAs, see the following article for your SSH client’s operating system:

For a Linux package-based Agent, multiple means of command-line access may be available, depending on the configuration of the machine. If you do not have SSH access with root or sudo privileges, please refer this article to your system administrator.

ThousandEyes VAs that have connectivity to the Internet will automatically download and install security patches. You may confirm the system has been patched using the aforementioned test command, validating against the expected responses.

Linux package-based Enterprise Agents should be patched according to the instructions for the particular Linux distribution. Consult your distribution’s documentation or support web site to determine the appropriate remediation steps for your distribution of Linux. We strongly recommend implementing automatic security updates for Linux systems. Consult your distribution's documentation for implementation instructions of automatic security updates.

Our team has excerpted remediation steps below, which will bring the Bash version up to date below, for Enterprise Agent-supported operating systems. As always, it is advisable to verify closure of the vulnerability once the update has been made.

#### Ubuntu-Based Remediation: <a href="#ubuntu-based-remediation" id="ubuntu-based-remediation"></a>

$ (sudo) apt-get install bash

#### RedHat Enterprise Linux/CentOS-Based Remediation: <a href="#redhat-enterprise-linux-centos-based-remediation" id="redhat-enterprise-linux-centos-based-remediation"></a>

$ (sudo) yum install bash
