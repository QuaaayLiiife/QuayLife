# Upgrading to BrowserBot 2

BrowserBot 2 introduces a containerized runtime environment for page load and transaction tests that is orchestrated using

[Podman](https://podman.io/)

. In doing so, it improves the consistency of browser-based test results and paves the way for new configuration options in page load and transaction tests.

Depending on the specifics of your Enterprise Agent deployments, you may need to take action prior to the rollout of BrowserBot 2. This article gives installation type- and OS-specific instructions.

If you need more time to complete these steps before the January 10, 2022 rollout, you may consider disabling agent updates until you are able to do so. A brief guide for that is included

[below](broken-reference)

.

### Preparing Enterprise Agents for the BrowserBot Update <a href="#preparing-enterprise-agents-for-the-browserbot-update" id="preparing-enterprise-agents-for-the-browserbot-update"></a>

All Docker agents running page load or transaction tests need to meet the following requirements before updating to BrowserBot 2:

* Their reported image version must be `0.14-1635966276` (or newer).
* They must be installed with appropriate AppArmor, seccomp, and/or SELinux configuration.

A guide to fulfilling each requirement is provided below.

**Updating to Image Version 0.14-1635966276 or Newer**

To inspect the image version of a Docker agent, go to **Cloud & Enterprise Agents > Agent Settings** and click the agent's row to expand the agent's configuration modal. A conforming Docker agent is shown below. If your Docker agent does not indicate an image version, it is too old to support BrowserBot 2 and must be upgraded.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1dbca9f925571039869d2407a6a77c58cc9148f3%2Fproduct-documentation\_global-vantage-points\_enterprise-agents\_upgrading-to-browserbot-2\_1.png?alt=media)

**Installing with Appropriate AppArmor, Seccomp, and/or SELinux Configuration**

To ensure your Docker host is set up with the appropriate AppArmor, seccomp, and/or SELinux configuration, use the instructions in

[Reinstalling the Enterprise Agent](<../../.gitbook/assets/enterprise agent deployment using docker (1)>)

. The requirements are the same as were previously required for Docker agents running transaction tests. Beginning with BrowserBot 2, these configurations are also required for Docker agents running page load tests.

**Red Hat Enterprise Linux (RHEL), CentOS, and Oracle Linux**

For Linux package agents running on **version 7.X** of RHEL and Oracle Linux distributions, you must make the following changes before your agents can upgrade to BrowserBot 2:

Additionally, users deploying BrowserBot 2 on RHEL, CentOS, or Oracle Linux may wish to review certain SELinux-related configurations that will be automatically installed on upgrade.

**Enabling the "extras" package repository**

This requirement only applies to RHEL 7.X and Oracle Linux 7.X distributions.

In order to install Podman and its dependencies, agents on RHEL 7.X and Oracle Linux 7.X distributions must enable an officially distributed "server extras" repository that is not enabled by default. The repository's name and how to enable it is provided for each OS below:

* RHEL 7.X: `subscription-manager repos --enable=rhel-7-server-extras-rpms`
* Oracle Linux 7.X: `yum-config-manager -q -y --enable ol7_addons`

Until this repository is enabled, BrowserBot will fail to upgrade to version 2.

This section is informational and requires no action on the part of users.

On CentOS 7.X, RHEL 7.X/8.X, and Oracle Linux 7.X/8.X enterprise agents, BrowserBot 2's package installation scripts will make two SELinux configuration changes that enable Page Load and Transaction tests to run while SELinux is in targeted enforcing mode. These changes are:

* An SELinux policy module called **te-browserbot**
* An SELinux file context equivalency rule between **/var/lib/containers** and **/var/lib/containers/te-browserbot-podman**

The **te-browserbot** policy module is installed at **/usr/share/selinux/packages/te-browserbot.pp.bz2** and allows the **te-browserbot-podman-proxy.service** process to communicate with the UNIX domain socket opened by **te-browserbot-podman.service**.

The file context equivalency rule tells SELinux to treat **/var/lib/containers/te-browserbot-podman** (the non-standard `--root` and `--runroot` location used by BrowserBot's podman daemon) the same as **/var/lib/containers** (the standard `--root` location used by Podman). This is important because the **container-selinux** package (an open-source, transitive dependency of `podman`) assumes that all Podman runtimes are configured with `--root=/var/lib/containers`. BrowserBot's file context equivalency rule applies **container-selinux**'s runtime-hardening SELinux policies to BrowserBot's non-standard Podman configuration.

Both the policy module and the file context rule are installed by the **te-browserbot** RPM package and are removed when **te-browserbot** is removed. Their presence on an Enterprise Agent can be confirmed as follows:

\[\[email protected]bbot /]# semanage fcontext -l | grep /var/lib/containers/te-browserbot-podman

/var/lib/containers/te-browserbot-podman = /var/lib/containers

container.pp.bz2 te-browserbot.pp.bz2

​

[On November 16, 2021](https://docs.thousandeyes.com/whats-new/changelog#2021-11-16)

, we announced the end of support for installing BrowserBot on Amazon Linux 2. While BrowserBot 1 installations will continue to work, we anticipate that these agents will not upgrade to BrowserBot 2.

Follow the steps below to disable auto-updates on your Enterprise Agent. By doing so, you can ensure that your agent won't be automatically upgraded to BrowserBot 2 in the January 10th rollout. This should only be done as a temporary measure, however; we recommend re-enabling auto-updates so that your agent receives important security and bug fixes, and so that it remains eligible for continued support.

1.  1\.

    Establish a shell in your Docker agent using `docker exec -it ${CONTAINER_NAME} bash`
2.  2\.

    Using `vim`, modify `/etc/te-agent.cfg` to include the line `auto-updates=0`
3.  3\.

    Restart `te-agent` with `sv restart te-agent`
4.  1\.

    Using `vim`, modify `/etc/te-agent.cfg` to include the line `auto-updates=0`
5.  2\.

    Restart `te-agent` with `sudo systemctl restart te-agent`

### Verifying the Upgrade to BrowserBot 2 <a href="#verifying-the-upgrade-to-browserbot-2" id="verifying-the-upgrade-to-browserbot-2"></a>

Please check the following to ensure that your Enterprise Agent has successfully upgraded to BrowserBot 2:

1.  1\.

    Check that the BrowserBot version visible in the Agent Settings page begins with a "2"
2.  2\.

    Confirm that the `te-sandboxd` process is no longer running: `ps aux | grep te-sandboxd`
3.  3\.

    Run an instant Page Load or Transaction test using the default configuration. Simply enter "https://www.google.com" as the URL and click "Run Once." If no "Internal Error" is shown for your Enterprise Agent, then the upgrade should be successful.
