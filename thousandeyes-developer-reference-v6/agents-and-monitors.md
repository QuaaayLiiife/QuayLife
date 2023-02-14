# Agents & Monitors

### Agents & Monitors

[`GET /v6/agents` Agent list](broken-reference)

Returns a list of all agents available to your account in ThousandEyes, including both Enterprise and Cloud agents.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `agentTypes=CLOUD|ENTERPRISE|ENTERPRISE_CLUSTER` optional, specifies the type of agents requested. Accepts either a single allowed value or a comma-separated list of allowed values
* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/agents.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of agents, specifying agentId, which can be used by other areas of the API. The agent’s public IP addresses will be shown, along with last. If an agent is an Enterprise agent, the agent’s public and private IP addresses will be shown, as well as the public network in which the agent is located.

| Field            | Data Type | Units      | Notes                                                                                                                                                                                                                                  |
| ---------------- | --------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId          | integer   | n/a        | unique ID of agent                                                                                                                                                                                                                     |
| agentName        | string    | n/a        | display name of the agent                                                                                                                                                                                                              |
| agentType        | string    | n/a        | Cloud, Enterprise or Enterprise Cluster, shows the type of agent                                                                                                                                                                       |
| countryId        | string    | n/a        | ISO-3166-1 alpha-2 country code of the agent                                                                                                                                                                                           |
| clusterMembers   | array     | n/a        | if an enterprise agent is clustered, detailed information about each cluster member will be shown as array entries in the clusterMembers field. This field is not shown for Enterprise Agents in standalone mode, or for Cloud Agents. |
| ipAddresses      | array     | n/a        | array of ipAddress entries                                                                                                                                                                                                             |
| groups           | array     | n/a        | array of label objects - see Labels for more information.                                                                                                                                                                              |
| location         | string    | n/a        | location of the agent                                                                                                                                                                                                                  |
| errorDetails     | array     | n/a        | if an enterprise agent or a cluster member presents at least one error, the errors will be shown as an array of entries in the errorDetails field (Enterprise Agents and Enterprise Cluster members only)                              |
| hostname         | string    | n/a        | fully qualified domain name of the agent (Enterprise Agents only)                                                                                                                                                                      |
| prefix           | string    | n/a        | Network prefix, expressed in CIDR format (Enterprise Agents only)                                                                                                                                                                      |
| enabled          | boolean   | n/a        | 1 for enabled, 0 for disabled (Enterprise Agents only)                                                                                                                                                                                 |
| network          | string    | n/a        | name of the autonomous system in which the Agent is found (Enterprise Agents only)                                                                                                                                                     |
| createdDate      | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, expressed in UTC. For Enterprise Clusters, this equals to the `createdDate` value of the initial cluster member before the conversion to cluster was performed (Enterprise Agents and Enterprise Clusters only)   |
| lastSeen         | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, expressed in UTC (Enterprise Agents only)                                                                                                                                                                         |
| agentState       | string    | n/a        | `Online`, `Offline` or `Disabled` (standalone Enterprise Agents only)                                                                                                                                                                  |
| keepBrowserCache | boolean   | n/a        | 1 for enabled, 0 for disabled (Enterprise Agents and Enterprise Clusters only)                                                                                                                                                         |
| utilization      | integer   | percentage | shows overall utilization percentage (online Enterprise Agents and Enterprise Clusters only)                                                                                                                                           |
| ipv6Policy       | string    | n/a        | IP version policy, can be `FORCE_IPV4`, `PREFER_IPV6` or `FORCE_IPV6` (Enterprise Agents and Enterprise Clusters only)                                                                                                                 |
| targetForTests   | string    | n/a        | target IP address or domain name representing test destination when agent is acting as a test target in an agent-to-agent test (Enterprise Agents only)                                                                                |

If the AgentType is `Enterprise Cluster`, a clusterMembers field will be available, which is an array of `clusterMember` objects, containing the following fields:

| Field             | Data Type | Units      | Notes                                                                                                                          |
| ----------------- | --------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------ |
| memberId          | integer   | n/a        | unique ID of the cluster member                                                                                                |
| name              | string    | n/a        | name of the cluster member                                                                                                     |
| ipAddresses       | array     | n/a        | array of ipAddress entries                                                                                                     |
| publicIpAddresses | array     | n/a        | array of ipAddress entries                                                                                                     |
| prefix            | string    | n/a        | Network prefix, expressed in CIDR format (Enterprise Agents only)                                                              |
| network           | string    | n/a        | name of the autonomous system in which the Agent is found (Enterprise Agents only)                                             |
| lastSeen          | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, expressed in UTC (Enterprise Agents only)                                                                 |
| agentState        | string    | n/a        | `Online`, `Offline` or `Disabled`                                                                                              |
| utilization       | integer   | percentage | shows overall utilization percentage of a cluster member                                                                       |
| targetForTests    | string    | n/a        | target IP address or domain name representing test destination when agent is acting as a test target in an agent-to-agent test |

If an `Enterprise Agent` or a `Cluster Member` presents at least one error, an errorDetails field will be available, which is an array of `errorDetail` objects, containing the following fields:

| Field       | Data Type | Units | Notes                                                                                                                                                                                                    |
| ----------- | --------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code        | string    | n/a   | `AGENT_VERSION_OUTDATED`, `APPLIANCE_VERSION_OUTDATED`, `BROWSERBOT_VERSION_OUTDATED`, `CLOCK_OFFSET`, `NAT_TRAVERSAL_ERROR`, `OS_END_OF_INSTALLATION_SUPPORT`, `OS_END_OF_SUPPORT`, or `OS_END_OF_LIFE` |
| description | string    | n/a   | detailed explanation of the error code                                                                                                                                                                   |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 6, "agentName": "Fremont, CA (v6)", "agentType": "Cloud", "countryId": "US", "ipAddresses": [ "2600:3c01::f03c:91ff:feae:4f96" ], "location": "San Francisco Area" }, { "agentId": 11, "agentName": "London, UK", "agentType": "Cloud", "countryId": "GB", "ipAddresses": [ "176.58.99.46", "178.79.138.106" ], "location": "City of London, United Kingdom" }, { "agentId": 29, "agentName": "Sample Enterprise Agent", "location": "United States", "countryId": "US", "createdDate": "2015-02-05 21:23:33", "prefix": "38.0.0.0/8", "ipAddresses": [ "10.100.50.25" ], "publicIpAddresses": [ "38.122.6.66" ], "network": "Cogent Communications (AS 174)", "agentType": "Enterprise", "lastSeen": "2015-02-05 23:23:33", "agentState": "Online", "targetForTests": "1.1.1.1" }, { "agentId": 1975, "agentName": "Duke cluster", "location": "San Francisco Bay Area", "countryId": "US", "createdDate": "2015-02-05 21:23:33", "enabled": 1, "keepBrowserCache": 0, "clusterMembers": [ { "name": "duke_agent3.thousandeyes.net", "ipAddresses": [ "172.17.0.2" ], "publicIpAddresses": [ "38.122.6.66" ], "prefix": "38.0.0.0/8", "utilization": 1, "network": "Cogent Communications (AS 174)", "lastSeen": "2015-07-15 17:16:11", "agentState": "Online", "memberId": 1235, "targetForTests": "2.2.2.2" }, [...] ], "agentType": "Enterprise Cluster", "utilization": 1, "ipv6Policy": "FORCE_IPV4" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/agents/{agentId}` Agent detail](broken-reference)

Returns details for an agent, including assigned tests. Enterprise agents show utilization data and assigned accounts.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/agents/12.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back agent details for an agent. For Enterprise Agents, additional details, including a list of account groups to which the agent is assigned, and utilization details will be shown. Metadata is shown below:

| Field             | Data Type | Units      | Notes                                                                                                                                                                                                                                  |
| ----------------- | --------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId           | integer   | n/a        | unique ID of agent                                                                                                                                                                                                                     |
| agentName         | string    | n/a        | display name of the agent                                                                                                                                                                                                              |
| location          | string    | n/a        | location of the agent                                                                                                                                                                                                                  |
| countryId         | string    | n/a        | ISO-3166-1 alpha-2 country code of the agent                                                                                                                                                                                           |
| clusterMembers    | array     | n/a        | if an enterprise agent is clustered, detailed information about each cluster member will be shown as array entries in the clusterMembers field. This field is not shown for Enterprise Agents in standalone mode, or for Cloud Agents. |
| prefix            | string    | n/a        | Network prefix, expressed in CIDR format (Enterprise Agents only)                                                                                                                                                                      |
| utilization       | integer   | percentage | shows overall utilization percentage (online Enterprise Agents and Enterprise Clusters only)                                                                                                                                           |
| ipv6Policy        | string    | n/a        | IP version policy, can be `FORCE_IPV4`, `PREFER_IPV6` or `FORCE_IPV6` (Enterprise Agents and Enterprise Clusters only)                                                                                                                 |
| ipAddresses       | array     | n/a        | array of ipAddress entries                                                                                                                                                                                                             |
| groups            | array     | n/a        | array of label objects - see Labels for more information.                                                                                                                                                                              |
| enabled           | boolean   | n/a        | 1 for enabled, 0 for disabled                                                                                                                                                                                                          |
| accountGroups     | array     | n/a        | list of account groups to which the agent is assigned, showing aid and accountGroupName fields (Enterprise Agents and Enterprise Clusters only)                                                                                        |
| tests             | array     | n/a        | list of tests assigned to the agent, expressed in the same format as `/tests` endpoint                                                                                                                                                 |
| network           | string    | n/a        | name of the autonomous system in which the Agent is found                                                                                                                                                                              |
| agentType         | string    | n/a        | either Cloud, Enterprise, or Enterprise Cluster, shows the type of agent                                                                                                                                                               |
| errorDetails      | array     | n/a        | if an enterprise agent or a cluster member presents at least one error, the errors will be shown as an array of entries in the errorDetails field (Enterprise Agents and Enterprise Cluster members only)                              |
| hostname          | string    | n/a        | fully qualified domain name of the agent (Enterprise Agents only)                                                                                                                                                                      |
| createdDate       | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, expressed in UTC. For Enterprise Clusters, this equals to the `createdDate` value of the initial cluster member before the conversion to cluster was performed (Enterprise Agents and Enterprise Clusters only)   |
| lastSeen          | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, expressed in UTC (Enterprise Agents only)                                                                                                                                                                         |
| agentState        | string    | n/a        | `Online`, `Offline` or `Disabled` (standalone Enterprise Agents only)                                                                                                                                                                  |
| notificationRules | array     | n/a        | array of notification rule objects configured on agent                                                                                                                                                                                 |
| keepBrowserCache  | boolean   | n/a        | 1 for enabled, 0 for disabled (Enterprise Agents and Enterprise Clusters only)                                                                                                                                                         |
| targetForTests    | string    | n/a        | target IP address or domain name representing test destination when agent is acting as a test target in an agent-to-agent test (Enterprise Agents only)                                                                                |

If the AgentType is `Enterprise Cluster`, a clusterMembers field will be available, which is an array of `clusterMember` objects, containing the following fields:

| Field             | Data Type | Units      | Notes                                                                                                                          |
| ----------------- | --------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------ |
| memberId          | integer   | n/a        | unique ID of the cluster member                                                                                                |
| name              | string    | n/a        | name of the cluster member                                                                                                     |
| ipAddresses       | array     | n/a        | array of ipAddress entries                                                                                                     |
| publicIpAddresses | array     | n/a        | array of ipAddress entries                                                                                                     |
| prefix            | string    | n/a        | Network prefix, expressed in CIDR format (Enterprise Agents only)                                                              |
| network           | string    | n/a        | name of the autonomous system in which the Agent is found (Enterprise Agents only)                                             |
| lastSeen          | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, expressed in UTC (Enterprise Agents only)                                                                 |
| agentState        | string    | n/a        | `Online`, `Offline` or `Disabled`                                                                                              |
| utilization       | integer   | percentage | shows overall utilization percentage of a cluster member                                                                       |
| targetForTests    | string    | n/a        | target IP address or domain name representing test destination when agent is acting as a test target in an agent-to-agent test |

If an `Enterprise Agent` or a `Cluster Member` presents at least one error, an errorDetails field will be available, which is an array of `errorDetail` objects, containing the following fields:

| Field       | Data Type | Units | Notes                                                                                                                                                                                                    |
| ----------- | --------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code        | string    | n/a   | `AGENT_VERSION_OUTDATED`, `APPLIANCE_VERSION_OUTDATED`, `BROWSERBOT_VERSION_OUTDATED`, `CLOCK_OFFSET`, `NAT_TRAVERSAL_ERROR`, `OS_END_OF_INSTALLATION_SUPPORT`, `OS_END_OF_SUPPORT`, or `OS_END_OF_LIFE` |
| description | string    | n/a   | detailed explanation of the error code                                                                                                                                                                   |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 12, "agentName": "San Po Kong, Hong Kong", "agentType": "Cloud", "countryId": "HK", "groups": [ { "groupId": -2, "name": "Cloud" }, { "groupId": -3, "name": "IPv4 Compatible" } ], "location": "Hong Kong", "tests": [ { "alertsEnabled": 1, "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/tests/822", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/dns/dnssec/822", "rel": "data" } ], "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 20:48:01", "domain": "thousandeyes.com A", "enabled": 1, "interval": 900, "liveShare": 0, "savedEvent": 0, "testId": 822, "testName": "thousandeyes.com A", "type": "dns-dnssec" }, ... ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/agents/{agentId}/update` Updating an agent](broken-reference)

Updates Enterprise Agent details. Users can update the agent parameters specified under Post Data section.

This endpoint can only be used for Enterprise Agents, and only for users in a role that permits modification of Enterprise Agents.

Important notes related to agent modification on tests:

* if an agent is removed from a test, the modification date for tests using that agent at the time it was removed will be changed.
* If an agent is removed from an entire account group, then all tests using this agent in the removed account group will be updated to reflect the removed agent.
* If a removed agent is the final remaining agent on a test, then the test will be disabled when the agent is removed.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agentId}` corresponds the unique ID of an enterprise agent, obtained from the `/agents` endpoint

#### Post Data <a href="#post_data" id="post_data"></a>

When POSTing data to the `/agents/{agentId}/update` endpoint, users can update the following fields:

* `agentName` string representation of an agent. No two agents can have the same display name.
* `enabled` boolean representation of agent state. `0` to disable the agent, `1` to enable the agent.
* `accountGroups` an array of accountGroup objects containing only an aid value, in the format { aid: integer }. See `/accounts` to pull a list of account IDs
* `tests` an array of test objects containing only a testId value in the format { testId: integer }. See `/tests` to pull a list of tests available in the current account context.
* `ipv6Policy` string representation of the IP version policy. Can be `FORCE_IPV4`, `PREFER_IPV6` or `FORCE_IPV6`.
* `keepBrowserCache` boolean representation of Keep browser cache state. `0` to disable, `1` to enable.
* `targetForTests` string representation of target IP address or domain name, representing test destination when agent is acting as a test target in an agent-to-agent test

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/agents/966/update.json \ -d '{ "agentName": "my updated agent name", "accountGroups": [ {"aid": 315}, {"aid": 362} ], "tests": [ {"testId": 12065} {"testId": 817}, ], "targetForTests":"1.2.3.4" }' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If an agent is successfully edited, an HTTP/200 OK response will be returned, and the agent’s assigned accounts / tests will change; the newly updated agent data will be returned. See the example below:

| Field            | Data Type | Units      | Notes                                                                                                                          |
| ---------------- | --------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------ |
| agentId          | integer   | n/a        | unique ID of agent                                                                                                             |
| agentName        | string    | n/a        | display name of the agent                                                                                                      |
| location         | string    | n/a        | location of the agent                                                                                                          |
| countryId        | string    | n/a        | ISO-3166-1 alpha-2 country code of the agent                                                                                   |
| prefix           | string    | n/a        | Network prefix, expressed in CIDR format                                                                                       |
| keepBrowserCache | boolean   | n/a        | `1` for enabled, `0` for disabled                                                                                              |
| utilization      | integer   | percentage | shows overall utilization percentage                                                                                           |
| ipv6Policy       | string    | n/a        | IP version policy, can be `FORCE_IPV4`, `PREFER_IPV6` or `FORCE_IPV6`                                                          |
| ipAddresses      | array     | n/a        | array of `ipAddress` entries                                                                                                   |
| groups           | array     | n/a        | array of label objects - see Labels for more information.                                                                      |
| enabled          | boolean   | n/a        | `1` for enabled, `0` for disabled                                                                                              |
| accountGroups    | array     | n/a        | list of account groups to which the agent is assigned, expressed in the same format as `/account-groups` endpoint              |
| tests            | array     | n/a        | list of tests assigned to the agent, expressed in the same format as `/tests` endpoint                                         |
| network          | string    | n/a        | name of the autonomous system in which the Agent is found                                                                      |
| agentType        | string    | n/a        | either `Cloud` or `Enterprise`, shows the type of agent                                                                        |
| lastSeen         | dateTime  | n/a        | `yyyy-MM-dd hh:mm:ss`, expressed in UTC                                                                                        |
| agentState       | string    | n/a        | either `Online` or `Offline`                                                                                                   |
| targetForTests   | string    | n/a        | target IP address or domain name representing test destination when agent is acting as a test target in an agent-to-agent test |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 966, "agentName": "ubuntu1404-x64", "location": "San Francisco Bay Area", "countryId": "US", "prefix": "50.128.0.0/9", "utilization": 1, "ipv6Policy": "FORCE_IPV4", "network": "Comcast Cable Communications, Inc. (AS 7922)", "agentType": "Enterprise", "lastSeen": "2015-05-14 23:18:00", "agentState": "Online", "keepBrowserCache": 1, "targetForTests": "1.1.1.1", "ipAddresses": [ "192.168.1.223" ], "publicIpAddresses": [ "50.184.189.59" ], "enabled": 1, "accountGroups": [ { "aid": 315, "accountGroupName": "Documentation" }, { "aid": 362, "accountGroupName": "Enterprise Agents Dashboard" } ], "tests": [ { "createdDate": "2015-02-03 21:55:13", "modifiedDate": "2015-05-14 23:18:03", "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 12065, "testName": "My Google DNS test", "type": "dns-server", "interval": 300, "domain": "google.com A", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "alertsEnabled": 0, "liveShare": 0, "recursiveQueries": 0, "dnsServers": [ { "serverId": 130, "serverName": "ns2.google.com." } ], "apiLinks": [...] }, { "enabled": 1, "testId": 817, "savedEvent": 0, "liveShare": 0, "testName": "http://www.thousandeyes.com", "type": "http-server", "interval": 900, "url": "http://www.thousandeyes.com", "networkMeasurements": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "modifiedDate": "2015-05-14 23:18:03", "apiLinks": [...] } ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/agents/{agentId}/delete` Deleting an Agent](broken-reference)

Deletes an Enterprise Agent from ThousandEyes. Note: this feature can only be used on Enterprise Agents.

Important notes related to agent removal:

* if an agent is deleted, the modification date for tests using that agent at the time it was deleted will be changed.
* If a deleted agent is the final remaining agent on a test, then the test will be disabled when the agent is removed.

Important note: if an agent is removed, it must be re-initialized to use the same machine again in different context. Virtual Appliances can be updated using the Reset State button in the Advanced tab of the agent management interface. Users running packaged versions of Linux will need to remove `/var/lib/te-agent/\*.sqlite` in order to reinitialize an agent.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agentId}` corresponds the unique ID of an enterprise agent, obtained from the `/agents` endpoint

#### Post Data <a href="#post_data" id="post_data"></a>

When POSTing data to the `/agents/{agentId}/delete` endpoint, users should specify an empty POST body.

#### Example <a href="#example" id="example"></a>

`$ curl -i https://api.thousandeyes.com/v6/agents/966/delete.json \ -d '' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If an agent is successfully deleted, an HTTP/204 No Content response will be returned, and an empty JSON response will be in the body of the response.

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

* The body of a delete request will be empty.

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/agents/{agentId}/add-to-cluster` Agent cluster - Creating](broken-reference)

Converts a standalone Enterprise Agent (or multiple) to an Enterprise Agent cluster.

This endpoint can only be used by users with the `Edit agents in account group` permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agentId}` in the request URL corresponds to the unique ID of an Enterprise Agent that is being converted to a cluster

Request notes:

* `{agentId}` can be obtained from the `/v6/agents` endpoint

**POST Data**

* The `agentId` present in the request URL must not be present in the POST body
* Each `agentId` must represent an agent of the `Enterprise` type (as shown by the `agentType` field in agent details)

**Example - converting a single agent**

`$ curl https://api.thousandeyes.com/v6/agents/64965/add-to-cluster.json \ -d '[]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

**Example - converting multiple agents**

`$ curl https://api.thousandeyes.com/v6/agents/64965/add-to-cluster.json \ -d '[ 70002, 70003 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

On successful cluster creation, the response will contain the following information:

* An HTTP/200 OK status
* The new cluster information will be provided in the response body
* Each cluster member will get a unique ID within a cluster, called `memberId`
* The `memberId` value is unrelated to the original `agentId` which was used in the request URL or POST body
* The cluster name will be taken from the agent whole `agentId` is present in the request URL

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 64965, "agentName": "apidoc-cluster1", "agentType": "Enterprise Cluster", "clusterMembers": [ { "memberId": 80001, "name": "apidoc-cluster1-agent1", // ... }, { "memberId": 80002, "name": "apidoc-cluster1-agent2", // ... }, { "memberId": 80003, "name": "apidoc-cluster1-agent3", // ... } ], // ... } ] }`

The example above is only showing contextually-relevant information. Full response metadata information is available in the [agent details API endpoint description](broken-reference).

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/agents/{agentId}/add-to-cluster` Agent cluster - Adding members](broken-reference)

Adds a new member (or multiple members) to an Enterprise Agent cluster.

This endpoint can only be used by users with the `Edit agents in account group` permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agentId}` in the request URL corresponds to the unique ID of an Enterprise Agent cluster to which new agent(s) will be added.

Request notes:

* `{agentId}` can be obtained from the `/v6/agents` endpoint.
* If the agent represented by the `{agentId}` is not already a cluster, it is converted to a cluster.

**POST Data**

* One or multiple (comma-separated) `agentId` values representing agents that should be added to the cluster, enclosed in square brackets.
* Each `agentId` must represent an agent of the `Enterprise` type (as shown by the `agentType` field in agent details).

**Example - adding one agent to a cluster**

`$ curl https://api.thousandeyes.com/v6/agents/64965/add-to-cluster.json \ -d '[ 80001 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

**Example - adding multiple agents to a cluster**

`$ curl https://api.thousandeyes.com/v6/agents/64965/add-to-cluster.json \ -d '[ 80001, 80002, 80003 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

On successful completion, the response will contain the following information:

* An HTTP/200 OK status
* The updated cluster information will be provided in the response body
* Each new cluster member will get a unique ID within a cluster, called `memberId`
* The `memberId` value is unrelated to the original `agentId` which was used in the request URL or POST body

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 64965, "agentName": "apidoc-cluster1", "agentType": "Enterprise Cluster", "clusterMembers": [ { "memberId": 80001, "name": "apidoc-cluster1-agent1", // ... }, { "memberId": 80002, "name": "apidoc-cluster1-agent2", // ... }, { "memberId": 80003, "name": "apidoc-cluster1-agent3", // ... } ], // ... } ] }`

The example above is only showing contextually-relevant information. Full response metadata information is available in the [agent details API endpoint description](broken-reference).

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/agents/{agentId}/remove-from-cluster` Agent cluster - Removing members](broken-reference)

Removes a member (or multiple members) from an Enterprise Agent cluster.

This endpoint can only be used for Enterprise Agent _clusters_, and only by users with the `Edit agents in account group` permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agentId}` in the request URL corresponds to the unique ID of an Enterprise Agent _cluster_ from which agent(s) will being removed.

Request notes:

* `{agentId}` can be obtained from the `/v6/agents` endpoint

**POST Data**

* One or multiple (comma-separated) `memberId` values representing agents that should be removed from the cluster, enclosed in square brackets.
* Cluster member IDs can be obtained from the `/v6/agents` API endpoint (the `memberId` field inside the `clusterMembers` array).

**Example - removing a single member**

`$ curl https://api.thousandeyes.com/v6/agents/64965/remove-from-cluster.json \ -d '[ 80001 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

**Example - removing multiple members**

`$ curl https://api.thousandeyes.com/v6/agents/64965/remove-from-cluster.json \ -d '[ 80002, 80003 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

On successful completion, the response will contain the following information:

* An HTTP/200 OK status
* The updated cluster information will be provided in the response body, unless all members are removed from the cluster
* Information about each removed member, now a standalone agent
* Each non-last member that has been removed from the cluster will get a new `agentId` value, unrelated to the `agentId` value the agent held before joining the cluster. The new `agentId` value is unrelated to the `memberId` value the agent held while it was a member of the cluster.
* If all members are removed from the cluster, the cluster itself is converted back to a standalone Enterprise Agent too. Such standalone agent inherits the old cluster’s `agentId` value. The last `memberId` listed in the POST body will be the one to inherit the cluster’s `agentId` value.

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 64965, "agentName": "apidoc-cluster1", "agentType": "Enterprise Cluster", "clusterMembers": [ { "memberId": 80001, "name": "apidoc-cluster1-agent1", } ], // ... }, { "agentId": 91112, "agentName": "apidoc-cluster1-agent2", "agentType": "Enterprise", // ... }, { "agentId": 91113, "agentName": "apidoc-cluster1-agent3", "agentType": "Enterprise", // ... } ] }`

The example above is only showing contextually-relevant information. Full response metadata information is available in the [agent details API endpoint description](broken-reference).

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/agents/{agentId}/remove-from-cluster` Agent cluster - Converting to an agent](broken-reference)

Converts a cluster with a single or multiple Enterprise Agent members back to a standalone Enterprise Agent(s).

This endpoint can only be used for Enterprise Agent _clusters_, and only by users with the `Edit agents in account group` permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agentId}` in the request URL corresponds to the unique ID of an Enterprise Agent _cluster_ being converted to a standalone Enterprise Agent(s).

Request notes:

* `{agentId}` can be obtained from the `/v6/agents` endpoint

**POST Data**

* One or multiple (comma-separated) `memberId` values representing all the agents that belong to and will be removed from the cluster, enclosed in square brackets.
* Cluster member IDs can be obtained from the `/v6/agents` API endpoint (the `memberId` field inside the `clusterMembers` array).

**Example - a single remaining cluster member**

`$ curl https://api.thousandeyes.com/v6/agents/64965/remove-from-cluster.json \ -d '[ 80001 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

**Example - disintegrating a cluster with multiple members**

`$ curl https://api.thousandeyes.com/v6/agents/64965/remove-from-cluster.json \ -d '[ 80001, 80002, 80003 ]' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

On successful completion, the response will contain the following information:

* An HTTP/200 OK status
* Information about each removed member, now a standalone agent
* Each non-last member that has been removed from the cluster will get a new `agentId` value, unrelated to the `agentId` value the agent held before joining the cluster. The new `agentId` value is unrelated to the `memberId` value the agent held while it was a member of the cluster.
* If all members are removed from the cluster, the cluster itself is converted back to a standalone Enterprise Agent too. Such standalone agent inherits the old cluster’s `agentId` value. The last `memberId` listed in the POST body will be the one to inherit the cluster’s `agentId` value.

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agents": [ { "agentId": 91111, "agentName": "apidoc-cluster1-agent1", "agentType": "Enterprise", // ... }, { "agentId": 91112, "agentName": "apidoc-cluster1-agent2", "agentType": "Enterprise", // ... }, { "agentId": 64965, "agentName": "apidoc-cluster1", "agentType": "Enterprise", // ... } ] }`

The example above is only showing contextually-relevant information. Full response metadata information is available in the [agent details API endpoint description](broken-reference).

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/bgp-monitors` BGP Monitor list](broken-reference)

Returns a list of all BGP monitors available to your account in ThousandEyes, including both public and private feeds.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/bgp-monitors.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of BGP monitors, including monitorId, which can be used by other areas of the API. The example below shows both a public and private BGP monitor.

| Field       | Data Type | Units | Notes                                                       |
| ----------- | --------- | ----- | ----------------------------------------------------------- |
| monitorId   | integer   | n/a   | unique ID of BGP monitor                                    |
| ipAddress   | string    | n/a   | IP address of the BGP monitor                               |
| network     | string    | n/a   | name of the autonomous system in which the monitor is found |
| monitorType | string    | n/a   | either Public or Private, shows the type of monitor         |
| monitorName | string    | n/a   | display name of the BGP monitor                             |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "bgpMonitors": [ { "ipAddress": "2001:240:100:ff::2497:2", "monitorId": 64, "monitorName": "Tokyo-3", "monitorType": "Public", "network": "Internet Initiative Japan Inc. (AS 2497)" }, { "ipAddress": "4.69.184.193", "monitorId": 1, "monitorName": "Seattle, WA", "monitorType": "Public", "network": "Level 3 Communications, Inc. (AS 3356)" }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/agent-notification-rules` Agent Notification Rules](broken-reference)

Returns a list of all agent notification rules configured under your account in ThousandEyes.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$curl https://api.thousandeyes.com/v6/agent-notification-rules.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object with one property. `agentAlertRules` is a collection of agent notification rule objects. Each object has the following properties:

| Field         | Data Type | Units | Notes                                                                                              |
| ------------- | --------- | ----- | -------------------------------------------------------------------------------------------------- |
| ruleId        | integer   | n/a   | unique ID of the agent notification rule                                                           |
| ruleName      | string    | n/a   | name of the agent notification rule                                                                |
| expression    | string    | n/a   | string expression of agent notification rule                                                       |
| notifyOnClear | boolean   | n/a   | 1 to send notification when notification clears                                                    |
| default       | boolean   | n/a   | when set to 1, agent notification rule will be automatically included on all new Enterprise agents |

`HTTP/1.1 200 OK Server: nginx Date: Tue, 11 Apr 2017 13:41:28 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1491918120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agentAlertRules": [ { "default": 1, "expression": "((clockOffset >= 60 s))", "notifyOnClear": 0, "ruleId": 1234, "ruleName": "Default Agent Clock Offset Notification" }, { "default": 1, "expression": "((lastContact >= 30 min))", "notifyOnClear": 0, "ruleId": 1244, "ruleName": "Default Agent Offline Notification" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/agent-notification-rules/{ruleId}` Agent Notification Rule Detail](broken-reference)

Returns details of an agent notification rule, including agents it is assigned to.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$curl https://api.thousandeyes.com/v6/agent-notification-rules/1234.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object with one property. `agentAlertRules` is a collection of agent notification rule objects. Each object has the following properties:

| Field         | Data Type  | Units | Notes                                                                                                                          |
| ------------- | ---------- | ----- | ------------------------------------------------------------------------------------------------------------------------------ |
| ruleId        | integer    | n/a   | unique ID of the agent notification rule                                                                                       |
| ruleName      | string     | n/a   | name of the agent notification rule                                                                                            |
| expression    | string     | n/a   | string expression of agent notification rule                                                                                   |
| notifyOnClear | boolean    | n/a   | 1 to send notification when notification clears                                                                                |
| default       | boolean    | n/a   | when set to 1, agent notification rule will be automatically included on all new Enterprise agents                             |
| agents        | collection | n/a   | list of agent objects this rule is assigned to                                                                                 |
| notifications | object     | n/a   | alert notification object; see [Alert notification integrations](https://developer.thousandeyes.com/v6/alerts/#/integrations). |

`HTTP/1.1 200 OK Server: nginx Date: Tue, 11 Apr 2017 13:41:58 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 598 X-Organization-Rate-Limit-Reset: 1491918120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "agentAlertRules": [ { "default": 1, "expression": "((lastContact >= 30 min))", "notifyOnClear": 0, "ruleId": 1234, "ruleName": "Default Agent Offline Notification", "notifications": { "email": { "message": "Test", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "channel": "@primoz", "integrationId": "sl-57", "integrationName": "Slack Primoz", "integrationType": "SLACK", "target": "https://hooks.slack.com/services/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" } ], "webhook": [ { "integrationId": "wb-41", "integrationName": "Test Hooks", "integrationType": "WEBHOOK", "target": "https://example.com/hook" } ] }, "agents": [ { "agentId": 3113, "agentName": "csc-statuspage", "agentState": "Disabled", "agentType": "Enterprise", "countryId": "US", "createdDate": "2017-03-31 04:33:52", "enabled": 0, "hostname": "csc-statuspage", "ipAddresses": [ "10.100.100.200" ], "ipv6Policy": "FORCE_IPV4", "keepBrowserCache": 0, "lastSeen": "2017-04-05 01:14:05", "location": "San Francisco Bay Area", "network": "Cogent Communications (AS 174)", "prefix": "38.0.0.0/8", "publicIpAddresses": [ "38.122.0.1" ], }, { "agentId": 3116, "agentName": "csc-ubuntu-docker", "agentState": "Disabled", "agentType": "Enterprise", "countryId": "US", "createdDate": "2017-03-31 04:34:11", "enabled": 0, "hostname": "csc-ubuntu-docker", "ipAddresses": [ "10.100.20.201" ], "ipv6Policy": "FORCE_IPV4", "keepBrowserCache": 0, "lastSeen": "2017-04-20 14:54:39", "location": "San Francisco Bay Area", "network": "Cogent Communications (AS 174)", "prefix": "38.0.0.0/8", "publicIpAddresses": [ "38.122.0.1" ], } ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
