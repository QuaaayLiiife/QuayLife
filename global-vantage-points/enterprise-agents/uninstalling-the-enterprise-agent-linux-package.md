# Uninstalling the Enterprise Agent (Linux Package)

Customers may need to remove the Enterprise Agent software which was installed on a supported Linux operating system from the **te-agent** and (optionally) **te-browserbot** packages. Additionally, customers may optionally remove the configuration files created by the agent. Customers may wish to keep the agent configuration files if the reason for removal is to fix a broken agent. Reinstalling agent software with existing configuration files allows the agent to resume running with the configuration of tests and other settings present prior to removing the agent software.

This article describes the steps required to remove an Enterprise Agent from each of the supported Linux distributions.

1.  1\.

    Check if the **te-agent** and the **te-browserbot** services are running:

    $ sudo systemctl status te-agent

    ● te-agent.service - ThousandEyes Agent

    Loaded: loaded (/lib/systemd/system/te-agent.service; enabled; vendor preset:

    Active: active (running) since Tue 2017-04-04 12:11:49 CDT; 2min 5s ago

    Main PID: 1052 (te-agent)

    CGroup: /system.slice/te-agent.service

    └─1052 /usr/local/bin/te-agent -C /etc/te-agent.cfg

    $ sudo service te-browserbot status

    ● te-browserbot.service - ThousandEyes BrowserBot

    Loaded: loaded (/lib/systemd/system/te-browserbot.service; enabled; vendor pr

    Active: active (running) since Tue 2017-04-04 12:12:16 CDT; 2min 17s ago

    CGroup: /system.slice/te-browserbot.service
2.  2\.

    Stop the **te-agent** and the **te-browserbot** services:

    $ sudo systemctl stop te-agent

    $ sudo systemctl status te-agent

    ● te-agent.service - ThousandEyes Agent

    Loaded: loaded (/lib/systemd/system/te-agent.service; enabled; vendor preset:

    Active: inactive (dead) since Tue 2017-04-04 12:16:29 CDT; 9s ago

    Process: 3632 ExecStart=/usr/local/bin/te-agent -C /etc/te-agent.cfg (code=kil

    Main PID: 3632 (code=killed, signal=TERM)

    $ sudo systemctl stop te-browserbot

    $ sudo systemctl status te-browserbot

    ● te-browserbot.service - ThousandEyes BrowserBot

    Loaded: loaded (/lib/systemd/system/te-browserbot.service; enabled; vendor pr

    Active: inactive (dead) since Tue 2017-04-04 12:17:03 CDT; 8s ago

    Process: 3696 ExecStart=/usr/bin/java -Djava.io.tmpdir=/var/lib/te-browserbot/

    Main PID: 3696 (code=exited, status=143)
3.  3\.

    Purge the **te-agent** and the **te-browserbot** packages: If you're planning to re-install the agent software use "apt-get remove" instead of "apt-get purge". This will leave the necessary configuration files intact, so that once the agent is re-installed, there is no need to re-assign tests to it.

    $ sudo apt-get purge te-agent

    Removing te-agent (1.9.1-1\~xenial) ...

    Updating certificates in /etc/ssl/certs...

    0 added, 0 removed; done.

    Running hooks in /etc/ca-certificates/update.d...

    Purging configuration files for te-agent (1.9.1-1\~xenial) ...

    Updating certificates in /etc/ssl/certs...

    0 added, 0 removed; done.

    Running hooks in /etc/ca-certificates/update.d...

    $ sudo apt-get purge te-browserbot

    (Reading database ... 68880 files and directories currently installed.)

    Removing te-browserbot (1.38-1\~xenial) ...

    Removing user \`browserbot' ...

    Warning: group \`browserbot' has no more members.
4.  4\.

    Verify that both packages have been removed:

    $ sudo systemctl status te-agent

    Loaded: not-found (Reason: No such file or directory)

    Active: inactive (dead) since Tue 2017-04-04 12:16:29 CDT; 7min ago

    Main PID: 3632 (code=killed, signal=TERM)

    $ sudo systemctl status te-browserbot

    Loaded: not-found (Reason: No such file or directory)

    Active: inactive (dead) since Tue 2017-04-04 12:17:03 CDT; 7min ago

    Main PID: 3696 (code=exited, status=143)

### RHEL/CentOS/Oracle Linux 6.x <a href="#rhel-centos-oracle-linux-6.x" id="rhel-centos-oracle-linux-6.x"></a>

1.  1\.

    Check if the **te-agent** and the **te-browserbot** services are running:

    te-agent start/running, process 17228

    te-browserbot start/running, process 17214
2.  2\.

    Stop the **te-agent** and the **te-browserbot** services:

    $ sudo stop te-browserbot

    te-browserbot stop/waiting
3.  3\.

    Remove the **te-agent** and the **te-browserbot** services:

    For those who wish to remove dependencies, use _yum erase_ instead of _yum remove:_

    $ sudo yum remove te-agent

    $ sudo yum remove te-browserbot
4.  4\.

    Verify that the **te-agent** and the **te-browserbot** services have been removed:

    status: Unknown job: te-agent

    status: Unknown job: te-browserbot

### RHEL/CentOS/Oracle Linux 7.x <a href="#rhel-centos-oracle-linux-7.x" id="rhel-centos-oracle-linux-7.x"></a>

1.  1\.

    Check if the **te-agent** and the t**e-browserbot** services are running:

    $ sudo systemctl status te-agent

    ● te-agent.service - ThousandEyes Agent

    Loaded: loaded (/usr/lib/systemd/system/te-agent.service; enabled; vendor preset: disabled)

    Active: active (running) since Thu 2017-03-30 11:31:35 EDT; 7s ago

    $ sudo systemctl status te-browserbot

    ● te-browserbot.service - ThousandEyes BrowserBot

    Loaded: loaded (/usr/lib/systemd/system/te-browserbot.service; enabled; vendor preset: disabled)

    Active: active (running) since Thu 2017-03-30 11:31:41 EDT; 5s ago
2.  2\.

    Stop the **te-agent** and the **te-browserbot** services:

    $ sudo systemctl stop te-agent

    $ sudo systemctl status te-agent

    ● te-agent.service - ThousandEyes Agent

    Loaded: loaded (/usr/lib/systemd/system/te-agent.service; enabled; vendor preset: disabled)

    Active: inactive (dead) since Thu 2017-03-30 11:25:12 EDT; 4min 46s ago

    $ sudo systemctl stop te-browserbot

    $ sudo systemctl status te-browserbot

    ● te-browserbot.service - ThousandEyes BrowserBot

    Loaded: loaded (/usr/lib/systemd/system/te-browserbot.service; enabled; vendor preset: disabled)

    Active: inactive (dead) since Thu 2017-03-30 11:28:25 EDT; 1min 40s ago
3.  3\.

    Remove the **te-agent** and the **te-browserbot** services:

    For those who wish to remove dependencies, use _yum erase_ instead of _yum remove._

    $ sudo yum remove te-agent

    te-agent.x86\_64 0:1.9.0-1

    $ sudo yum remove te-browserbot

    te-browserbot.x86\_64 0:1.38-1
4.  4\.

    Verify that the **te-agent** and the **te-browserbot** have been removed:

    $ systemctl status te-agent

    Unit te-agent.service could not be found.

    $ systemctl status te-browserbot

    Unit te-browserbot.service could not be found.

### Delete the Agent from the ThousandEyes Platform <a href="#delete-the-agent-from-the-thousandeyes-platform" id="delete-the-agent-from-the-thousandeyes-platform"></a>

If you do not plan to replace the agent, you should remove it from the ThousandEyes platform. From the **Agent Settings** page, expand the agent's row, then click the **More Actions** icon and select **Delete**.

**NOTE:** Deleting an agent will remove it from any tests to which it was assigned, and any tests that have no other agents assigned will be disabled.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-76792b7e0e8544006aa61a117ae211cb6b9afdd2%2Fproduct-documentation\_enterprise-agents\_uninstalling-the-enterprise-agent-linux-package-1.png?alt=media)
