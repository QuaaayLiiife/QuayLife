# ThousandEyes Infrastructure Changes

### ThousandEyes Infrastructure Changes <a href="#thousandeyes-infrastructure-changes" id="thousandeyes-infrastructure-changes"></a>

Starting on November 15th, 2020, ThousandEyes will transition its infrastructure from the current data center to Amazon Web Services. The new infrastructure will use new IP address spaces. ThousandEyes customers who have IP address-based access control lists (ACLs) or firewall rules to permit Enterprise Agents, Endpoint Agents or other resources to communicate specifically with the ThousandEyes infrastructure will need to update those ACLs or rules. New ACLs or rules for the new addresses must be added to the existing ACLs and rules no later than November 15th, 2020. Any ACLs or rules with the old IP addresses must remain in place and active until at least January 31st, 2021.

Customers who do not use ACLs or firewall rules to allow communications with ThousandEyes infrastructure do not need to take any action.

Customers who use ACLs or firewalls to allow communications with ThousandEyes Cloud Agents do not need to take any action.

[Cloud Agent IP addresses](https://docs.thousandeyes.com/product-documentation/api/obtaining-a-list-of-thousandeyes-agent-ip-addresses)

will not be modified in this transition.

This article provides a list of the new IP addresses for ThousandEyes infrastructure. The ThousandEyes article

[Firewall Configuration for Enterprise Agents](https://docs.thousandeyes.com/product-documentation/enterprise-agents/firewall-configuration-for-enterprise-agents)

contains the current list of addresses, and will be updated with the new addresses when the transition is complete.

#### Change Configuration Details <a href="#change-configuration-details" id="change-configuration-details"></a>

The tables below contain the domain names, current and new IP addresses of all publicly facing services in the ThousandEyes infrastructure. Customers may have ACLs, firewall or web application firewall (WAF) rules for all of the listed services or for only a subset of the full list.

The first table contains information for services requiring connections to the ThousandEyes infrastructure. These services include the ThousandEyes app, API and services used by ThousandEyes Agents to upload data. IP addresses or domain names in this table will appear as destinations in ACLs or rules.

The second table contains information for services requiring connections from the ThousandEyes infrastructure to customer services. These services implement the

[notifications and integrations](https://docs.thousandeyes.com/product-documentation/alerts/how-alerts-work#notifications)

features (specifically

[Webhooks](https://docs.thousandeyes.com/product-documentation/alerts/using-webhooks-server-sample-code-included)

,

[AppDynamics](https://docs.thousandeyes.com/product-documentation/alerts/integrations/appdynamics-integration)

,

[Slack](https://docs.thousandeyes.com/product-documentation/alerts/integrations/slack-integration)

,

[ServiceNow](https://docs.thousandeyes.com/product-documentation/alerts/integrations/servicenow-integration)

, and

[PagerDuty](https://docs.thousandeyes.com/product-documentation/alerts/integrations/pagerduty-integration)

) of the ThousandEyes app's alerts rules. IP addresses or domain names in this table will appear as sources in ACLs or rules.

To make the change to the new ThousandEyes infrastructure, review the possible configuration methods for ACLs or rules below to determine which method your organization uses, and the corresponding steps.

* Customers with ACLs, firewall or web application firewall (WAF) rules that use the IP addresses listed in the **Current Address(es)** column of the following tables will use the addresses listed in the **New Addresses** column to add the new ACLs or rules.
* Customers whose ACLs or rules use the ThousandEyes CIDR netblock **192.150.160.0/24** rather than the individual IP addresses listed in the **Current Address(es)** column _must_ use the individual addresses listed in the **New Addresses** column to add the new ACLs or rules. _The addresses in the new infrastructure do not fall within a single netblock or contiguous range._
* Customers with ACLs, firewall or web application firewall (WAF) rules which use DNS domain names rather than IP addresses will not need to make changes to domain names in those lists or rules. Depending on the implementation of your domain name-based controls, customers may need to take action to reload the rulesets with the new name-to-address mappings. Consult your security administrators or the documentation for your security devices to determine any steps required to reload domain name-based controls.

The tables below provide the information required to add new ACLs or rules. Customers can identify which domain names or IP addresses are needed based on the ThousandEyes product or service used. For example, customers who have Enterprise Agents but no Endpoint Agents can add ACLs or rules for all names or addresses except those in the Endpoint Agents section of the first table.

For customers unsure of which products or services their organization uses, we recommend adding ACLs or rules for all of the entries in both tables.

If adding rules for the second table requires greater review due to an organization's security policies and thus more effort to implement, customers can attempt to determine whether the second table's ACLs or rules are needed by consulting the ThousandEyes documentation on the alert rules feature's

[notifications and integrations](https://docs.thousandeyes.com/product-documentation/alerts/how-alerts-work#notifications)

features (specifically

[Webhooks](https://docs.thousandeyes.com/product-documentation/alerts/using-webhooks-server-sample-code-included)

,

[AppDynamics](https://docs.thousandeyes.com/product-documentation/alerts/integrations/appdynamics-integration)

,

[Slack](https://docs.thousandeyes.com/product-documentation/alerts/integrations/slack-integration)

,

[ServiceNow](https://docs.thousandeyes.com/product-documentation/alerts/integrations/servicenow-integration)

, and

[PagerDuty](https://docs.thousandeyes.com/product-documentation/alerts/integrations/pagerduty-integration)

) and then reviewing their configuration of notifications and integrations in their ThousandEyes account.

**NOTE:** Notifications and integrations are configured on a per-account group basis, so customers should review all account groups within an organization to locate any configured notifications or integrations. For organizations with large numbers of account groups, the ThousandEyes API can be used to query for a list of

[account group IDs](https://developer.thousandeyes.com/v6/#/accountcontext)

and then the

[list of notifications and integrations](https://developer.thousandeyes.com/v6/alerts/#/integrations)

per account group.

**Table 1: Connections from customer networks to ThousandEyes infrastructure**

Add ACLs or rules with destination IP addresses from the **New addresses** column (similar to any existing ACLs or rules with destination IP addresses in the **Current address(es)** column).

| Product/Service   | DNS Domain Name               | Current Address(es) | New Addresses                                                                     |
| ----------------- | ----------------------------- | ------------------- | --------------------------------------------------------------------------------- |
| ThousandEyes App  | app.thousandeyes.com          | 192.150.160.193     | <p>50.18.71.33</p><p>54.241.92.230</p><p>13.248.203.51</p><p>76.223.82.139</p>    |
| ​                 | \*.share.thousandeyes.com     | 192.150.160.195     | <p>50.18.147.222</p><p>54.177.244.79</p><p>13.248.217.17</p><p>76.223.69.131</p>  |
| ​                 | embed.thousandeyes.com        | 192.150.160.202     | <p>52.9.5.97</p><p>54.177.66.87</p><p>75.2.122.52</p><p>99.83.143.133</p>         |
| ThousandEyes API  | api.thousandeyes.com          | 192.150.160.194     | <p>54.177.34.231</p><p>54.193.142.147</p><p>13.248.200.34</p><p>76.223.86.189</p> |
| Enterprise Agents | c1.agt.thousandeyes.com       | 192.150.160.17      | <p>13.52.142.100</p><p>54.215.23.174</p><p>75.2.66.34</p><p>99.83.133.153</p>     |
| ​                 | sc1.thousandeyes.com          | 192.150.160.18      | <p>54.153.76.24</p><p>54.215.2.49</p><p>75.2.105.19</p><p>99.83.165.166</p>       |
| ​                 | data1.agt.thousandeyes.com    | 192.150.160.203     | <p>18.144.149.12</p><p>54.219.22.100</p><p>13.248.204.16</p><p>76.223.76.176</p>  |
| ​                 | ntrav.thousandeyes.com        | 192.150.160.20      | <p>54.176.41.14</p><p>54.241.50.7</p><p>75.2.27.3</p><p>99.83.136.191</p>         |
| ​                 | crashreports.thousandeyes.com | 192.150.160.50      | <p>204.236.190.123</p><p>54.241.250.221</p><p>75.2.49.1</p><p>99.83.242.129</p>   |
| Endpoint Agents   | c1.eb.thousandeyes.com        | 192.150.160.199     | <p>204.236.184.131</p><p>52.9.192.109</p><p>75.2.45.13</p><p>99.83.250.143</p>    |
| ​                 | data.eb.thousandeyes.com      | 192.150.160.200     | <p>50.18.29.173</p><p>54.176.79.58</p><p>13.248.210.21</p><p>76.223.72.156</p>    |

**Table 2: Connections to customer networks from ThousandEyes infrastructure**

Add ACLs or rules with source IP addresses from the **New addresses** column (similar to any existing ACLs or rules with source IP addresses in the **Current address(es)** column).

| Product/Service                           | DNS Domain Name | Current Addresses                          | New Addresses                         |
| ----------------------------------------- | --------------- | ------------------------------------------ | ------------------------------------- |
| Alert Rule Notifications and Integrations | Not applicable  | <p>192.150.160.12</p><p>192.150.160.13</p> | <p>52.52.142.26</p><p>52.52.36.83</p> |

For customers considering switching their IP address-based ACLs or rules to use domain names, be aware that the domain names are not currently protected by DNSSEC.

Customers should add the new IP addresses or DNS domain names by November 15th, 2020. Customers should allow sufficient time to submit these changes to any configuration or change control processes used in their organization. ACLs or rules with the old IP addresses must remain in place and active until at least January 31st, 2021 or until further notice.

As the date for the cutover approaches, consult this article or the ThousandEyes

[Changelog](https://docs.thousandeyes.com/whats-new/changelog)

for updates. Customers may also contact

ThousandEyes Customer Engineering

with questions or concerns, or contact us via in-app chat.
