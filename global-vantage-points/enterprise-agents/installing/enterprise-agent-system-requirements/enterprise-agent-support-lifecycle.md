# Enterprise Agent Support Lifecycle

In order to ensure proper and consistent data collection, ThousandEyes Enterprise Agents require up-to-date agent software, running on a fully supported operating system. As operating system providers end support for versions of their operating systems, ThousandEyes will reduce or end support for Enterprise Agents on those operating systems.

This article details the ThousandEyes support policy and notification methods, the stages of the ThousandEyes Enterprise Agent operating system and software support lifecycle, and the relevant end of life/support dates for each supported operating system.

### ThousandEyes Support Lifecycle Policy <a href="#thousandeyes-support-lifecycle-policy" id="thousandeyes-support-lifecycle-policy"></a>

ThousandEyes will take reasonable measures to provide customers with at least 90 days' advance notice in the event that any features or functions of the ThousandEyes service are deprecated or removed, if the removal of the feature may negatively impact a customer's use of the service. Notifications will be made via the

[Changelog](https://docs.thousandeyes.com/whats-new/changelog)

, as well as via email to any relevant

[email subscribers](https://docs.thousandeyes.com/product-documentation/alerts/notification-of-upgrades-maintenance-and-outages#subscribing-to-email-notifications)

.

ThousandEyes may make modifications on less than 90 days' advance notice if required to fix a security issue.

ThousandEyes reserves the right to modify this policy at our discretion.

For Enterprise Agents that have reached a new lifecycle phase, the **Operating System** text in the agent's entry in the

[Enterprise Agent Settings](https://app.thousandeyes.com/settings/agents/enterprise/?section=agents)

page of the ThousandEyes application will be displayed in red, with a link to the relevant upgrade documentation.

Approaching lifecycle phases are announced in the

[changelog](https://docs.thousandeyes.com/whats-new/changelog)

entries that accompany ThousandEyes software releases. Software releases typically occur every two weeks. Notification of an approaching phase change will appear in at least one changelog entry, typically at least a month in advance of the announced date.

#### Enterprise Agent Software Support <a href="#enterprise-agent-software-support" id="enterprise-agent-software-support"></a>

ThousandEyes provides technical support and software updates for issues found in versions of the Enterprise Agent software issued within six months of the most recent release date of agent software. To obtain fixes for Enterprise Agent software, customers must upgrade to the most recent version of Enterprise Agent software. Enterprise Agents normally perform software updates automatically when ThousandEyes makes an update available.

ThousandEyes Enterprise Agents run on either the Ubuntu Linux distribution, or the Red Hat Enterprise Linux distribution (along with the CentOS and Oracle Linux variations of Red Hat Enterprise Linux). The ThousandEyes support lifecycle contains four phases that are based on the supported Ubuntu Linux Long Term Support (LTS) versions and the Red Hat Enterprise Linux versions currently in either the **Full Support Phase** or the subsequent **Extended Update Support** (EUS) period.

There are four phases in the ThousandEyes support lifecycle:

* End of Installation Support

**End of Installation Support**

In the **End of Installation Support** (EIS) phase, ThousandEyes will remove the ability to install Enterprise Agents on a version of an operating system. This occurs three months prior to the **End of Support** phase.

In the **End of Support** (EoS) phase, ThousandEyes will no longer provide technical support nor guarantee software updates (including bug fixes) for customers running Enterprise Agents on the affected version of an operating system. Agents may continue to commit test data to the ThousandEyes platform.

**End of Life** (EoL) occurs 60 days after the **End of Support** phase begins. Agents will no longer be able to communicate with the ThousandEyes platform, and will self-terminate with an error message.

**Example Operating System Support Lifecycle**

The diagram below uses Ubuntu Linux version 14.04 LTS to illustrate the three phases of the ThousandEyes lifecycle. Support for version 14.04 LTS ended in April, 2019:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-019cae1ee850c88d0584f07a997c7747a150d1c8%2Fproduct-documentation\_enterprise-agents\_enterprise-agent-support-lifecycle-policy-1.png?alt=media)

### Operating System Lifecycle Phase Dates <a href="#operating-system-lifecycle-phase-dates" id="operating-system-lifecycle-phase-dates"></a>

The sections and tables below provide the upcoming lifecycle phase change dates for each currently supported operating system version.

ThousandEyes only supports Ubuntu Linux long term support (LTS) versions. Ubuntu supports LTS versions for five years after the release date. Once the Enterprise Agent software is released for a specific LTS version, ThousandEyes will align the start of its End of Support phase with the operating system's End of Life date, as defined by Ubuntu.

The Ubuntu Wiki

[Releases](https://wiki.ubuntu.com/Releases)

page lists their **End of Life** dates. The corresponding ThousandEyes lifecycle dates are listed below, using YYYY-MM-DD.

| Operating System Version    | End of Installation Support | End of Support | End of Life |
| --------------------------- | --------------------------- | -------------- | ----------- |
| Ubuntu 18.04 LTS (“Bionic”) | 2023-01-31                  | 2023-04-30     | 2023-06-30  |
| Ubuntu 20.04 LTS ("Focal")  | 2025-01-31                  | 2025-04-30     | 2025-06-30  |

#### Red Hat Enterprise Linux / CentOS / Oracle Linux <a href="#red-hat-enterprise-linux-centos-oracle-linux" id="red-hat-enterprise-linux-centos-oracle-linux"></a>

ThousandEyes supports versions of Red Hat Enterprise Linux (and the corresponding versions of CentOS and Oracle Linux) that are eligible for Red Hat's

[Extended Update Support Subscription](https://access.redhat.com/solutions/22763)

.

In most cases, ThousandEyes bases support for versions of Red Hat Enterprise Linux, CentOS, and Oracle Linux on Red Hat's EUS subscription schedule. ThousandEyes will end support for the major version (i.e. all minor versions including the most recent minor version) at the expiration of EUS for the last eligible minor version.

For more information on the EUS-eligible versions and EUS end dates, see

[Red Hat Enterprise Linux Life Cycle](https://access.redhat.com/support/policy/updates/errata)

. The corresponding ThousandEyes lifecycle dates are listed in the sections below.

**Red Hat Enterprise Linux / CentOS / Oracle Linux 7**

| Operating System Version | End of Installation Support | End of Support | End of Life |
| ------------------------ | --------------------------- | -------------- | ----------- |
| 7.8                      | 2024-04-01                  | 2024-06-30     | 2024-08-29  |
| 7.9                      | 2024-04-01                  | 2024-06-30     | 2024-08-29  |

**Red Hat Enterprise Linux / Oracle Linux 8**

| Operating System Version | End of Installation Support | End of Support | End of Life |
| ------------------------ | --------------------------- | -------------- | ----------- |
| 8.1                      | 2021-08-31                  | 2021-11-30     | 2022-01-30  |
| 8.2                      | 2022-01-31                  | 2022-04-30     | 2022-06-30  |
| 8.3                      | 2021-10-02                  | 2021-12-31     | 2022-03-01  |
| 8.4                      | 2023-03-01                  | 2023-05-30     | 2023-07-29  |
| 8.5                      | 2022-01-30                  | 2022-04-30     | 2022-06-29  |
| 8.6                      | 2024-03-01                  | 2024-05-30     | 2024-07-29  |
| 8.7                      | 2023-01-30                  | 2023-04-30     | 2023-06-29  |
| 8.8                      | 2025-03-01                  | 2025-05-30     | 2025-07-29  |
| 8.9                      | 2024-01-31                  | 2024-04-30     | 2024-06-29  |
| 8.10                     | 2029-03-01                  | 2029-05-30     | 2029-07-29  |

ThousandEyes will provide support for Amazon Linux until the operating system reaches **End of Life**, as defined by Amazon. For more information, see

[Amazon Linux 2 FAQs](https://aws.amazon.com/amazon-linux-2/faqs/)

.

The corresponding ThousandEyes lifecycle dates are listed below.

| Operating System Version | End of Installation Support | End of Support | End of Life |
| ------------------------ | --------------------------- | -------------- | ----------- |
| Amazon Linux 2           | 2023-03-30                  | 2023-06-30     | 2023-08-30  |
