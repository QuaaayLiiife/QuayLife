# ALERTS & NOTIFICATIONS

[`GET /v7/alerts` Active alerts](broken-reference)

Returns a list of all active alerts, or alerts that started within a given time range.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v7/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v7/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/alerts \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of presently active alerts, or alerts that became active during the time range specified. If the specific time range is requested, only the alerts that have triggered in that time range will be returned. If no alerts were triggered during the time range specified, an empty response will be returned.

| Field     | Data Type      | Units               | Notes                                                                                                                                                                                          |
| --------- | -------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertId   | integer        | n/a                 | unique ID of the alert; each alert occurrence is assigned a new unique ID                                                                                                                      |
| alertType | string         | n/a                 | type of alert being triggered. In multi-layered tests, this value represents the layer the alert relates to. See [Alert Details](broken-reference) documentation for a list of possible values |
| apiLinks  | array of links | n/a                 | list of hyperlinks to other areas of the API                                                                                                                                                   |
| dateStart | dateTime       | yyyy-MM-dd hh:mm:ss | the date/time where an alert rule was triggered, expressed in UTC                                                                                                                              |
| dateEnd   | dateTime       | yyyy-MM-dd hh:mm:ss | the date/time where the alert has cleared, expressed in UTC                                                                                                                                    |
| permalink | string         | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                    |
| ruleId    | integer        | n/a                 | unique ID of the alert rule (see `/alert-rules` endpoint for more detail)                                                                                                                      |
| state     | string         | n/a                 | current state of the alert. Possible values: `ACTIVE`, `CLEARED`, or `DISABLED` (when the test is deleted or disabled, or when the alert rule is deleted or disassociated from the test)       |
| severity  | string         | n/a                 | field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                       |

`HTTP/1.1 200 OK Date: Thu, 23 Apr 2020 13:09:28 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1587647400 Strict-Transport-Security: max-age=31536000`

**Body**

`{ "alerts": [ { "alertId": 2556232, "alertType": "http-server", "apiLinks": [ { "href": "https://api.thousandeyes.com/v7/alerts/http-server/2556232", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/alert-rules/289585.json", "rel": "rule" } ], "dateStart": "2020-04-23 13:43:16", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=7625&alertId=2556232", "ruleId": 289585, "state": "ACTIVE", "severity": "INFO" }, { "alertId": 2257070, "alertType": "network-outage", "apiLinks": [ ... ], "dateStart": "2020-02-20 07:45:00", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=7625&alertId=2257070", "ruleId": 186333, "state": "ACTIVE", "severity": "INFO" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`GET /v7/alerts/{alertType}/{alertId}` Alert details](broken-reference)

Returns details about an alert. The `{alertType}` value in URL must match specific alert???s type.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

**Example requests**

`$ curl https://api.thousandeyes.com/v7/alerts/bgp/1000001 \ -u {email}:{authToken}`

`$ curl https://api.thousandeyes.com/v7/alerts/http-server/1000002 \ -u {email}:{authToken}`

`$ curl https://api.thousandeyes.com/v7/alerts/network-outage/1000003 \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed information about a specific `alertId`. If the `alertId` doesn???t exist or is inaccessible by your account, an empty response will be returned.

| Field           | For alert type                                         | Data Type                 | Units               | Notes                                                                                                                                                                                                                                                                                      |
| --------------- | ------------------------------------------------------ | ------------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| agents          | CEA\* (except `bgp`)                                   | array of agent objects    | n/a                 | array of agents where the alert has at some point been active since the point that the alert was triggered                                                                                                                                                                                 |
| alertId         | (all)                                                  | integer                   | n/a                 | unique ID of the alert; each alert occurrence is assigned a new unique ID                                                                                                                                                                                                                  |
| alertType       | (all)                                                  | string                    | n/a                 | type of alert being triggered. In multi-layered tests, this value represents the layer the alert relates to                                                                                                                                                                                |
| apiLinks        | (all)                                                  | array of links            | n/a                 | list of hyperlinks to other areas of the API                                                                                                                                                                                                                                               |
| asName          | `network-outage`                                       | string                    | n/a                 | name of the Autonomous System                                                                                                                                                                                                                                                              |
| asn             | `network-outage`                                       | integer                   | n/a                 | number of the Autonomous System                                                                                                                                                                                                                                                            |
| dateEnd         | (all)                                                  | dateTime                  | yyyy-MM-dd hh:mm:ss | the date/time when the alert has cleared, expressed in UTC                                                                                                                                                                                                                                 |
| dateStart       | (all)                                                  | dateTime                  | yyyy-MM-dd hh:mm:ss | the date/time when an alert rule was triggered, expressed in UTC                                                                                                                                                                                                                           |
| locations       | `network-outage` and `application-outage`              | array of location objects | n/a                 | array of locations participating in an outage. Each entry represents a 5-minute interval, meaning if the same location is recognized as affected in two consecutive 5-minute rounds, two entries for the same location will be present in this array, with different `dateAffected` values |
| monitors        | `bgp`                                                  | array of monitor objects  | n/a                 | array of monitors where the alert has at some point been active since the point that the alert was triggered. Only shown on BGP alerts.                                                                                                                                                    |
| permalink       | (all)                                                  | string                    | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                                                                                |
| ruleId          | (all)                                                  | integer                   | n/a                 | unique ID of the alert rule (see `/alert-rules` endpoint for more detail)                                                                                                                                                                                                                  |
| state           | (all)                                                  | string                    | n/a                 | current state of the alert. Possible values: `ACTIVE`, `CLEARED`, or `DISABLED` (when the test is deleted or disabled, or when the alert rule is deleted or disassociated from the test)                                                                                                   |
| testId          | CEA                                                    | integer                   | n/a                 | unique ID of the test (see `/tests/{testId}` endpoint for more detail)                                                                                                                                                                                                                     |
| violationCount  | (all except `network-outage` and `application-outage`) | integer                   | n/a                 | number of sources currently meeting the alert criteria                                                                                                                                                                                                                                     |
| applicationName | `application-outage`                                   | string                    | n/a                 | name of the affected application                                                                                                                                                                                                                                                           |
| severity        | (all)                                                  | string                    | n/a                 | field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                                                                                                                   |

Abbreviations used in the table above: \* CEA: Cloud & Enterprise Agent-related tests

The `alertType` field will contain one of the following values:

| alertType            | Platform area | Entity | Related test layer/type or additional notes |
| -------------------- | ------------- | ------ | ------------------------------------------- |
| `bgp`                | CEA\*         | Tests  | Routing / BGP                               |
| `path-trace`         | CEA           | Tests  | Network / Path visualization data           |
| `end-to-end-server`  | CEA           | Tests  | Network / Agent to Server                   |
| `end-to-end-agent`   | CEA           | Tests  | Network / Agent to Agent                    |
| `dns-server`         | CEA           | Tests  | DNS / DNS Server                            |
| `dns-trace`          | CEA           | Tests  | DNS / DNS Trace                             |
| `dns-dnssec`         | CEA           | Tests  | DNS / DNSSEC                                |
| `http-server`        | CEA           | Tests  | Web / HTTP Server                           |
| `page-load`          | CEA           | Tests  | Web / Page Load                             |
| `web-transaction`    | CEA           | Tests  | Web / Transaction                           |
| `ftp-server`         | CEA           | Tests  | Web / FTP Server                            |
| `voice`              | CEA           | Tests  | Voice / RTP Stream                          |
| `sip-server`         | CEA           | Tests  | Voice / SIP Server                          |
| `network-outage`     | II\*          | -      | Network outage                              |
| `application-outage` | II\*          | -      | Application outage                          |

Abbreviations used in the table above:

* CEA: Cloud & Enterprise Agents
* II: Internet Insights

Agent objects (see above) reflect the following content:

| Field          | Data Type | Units               | Notes                                                                                                                                                                                                                                             |
| -------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId        | integer   | n/a                 | unique ID of agent or monitor violating the alert rule. See `/agents` for more detail                                                                                                                                                             |
| agentName      | string    | n/a                 | display name of the agent violating the alert rule                                                                                                                                                                                                |
| dateEnd        | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the earlier of the date that the alert was cleared, or the source reported a measurement that was under the alert rule???s threshold, expressed in UTC                                                                                     |
| dateStart      | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the date that the source began reporting a measurement that exceeded the alert rule???s threshold, expressed in UTC                                                                                                                        |
| metricsAtEnd   | string    | n/a                 | string representation of the metric or metrics being considered in the alert rule at the point that the alert was cleared. If the alert is not yet cleared, this field reflects the last round of data gathered from the source.                  |
| metricsAtStart | string    | n/a                 | string representation of the metric at the time that the source began alerting. Note that the alert start and dateStart for a particular source do not need to be the same, as sources may change alerting status throughout an alert???s lifecycle |
| permalink      | string    | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                                       |
| state          | string    | n/a                 | current state of the alert for this agent. Possible values: `ACTIVE`, `CLEARED`, or `DISABLED` (when the test is deleted or disabled, or when the alert rule is deleted or disassociated from the test)                                           |

Location objects (available for `network-outage` alert type only, see above) reflect the following content:

| Field                   | Data Type         | Units               | Notes                                                                                                                 |
| ----------------------- | ----------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| affectedInterfacesCount | integer           | n/a                 | number of affected router interfaces by this outage                                                                   |
| affectedTests           | array of integers | n/a                 | array of affected `testId`s in the current account group                                                              |
| affectedTestsCount      | integer           | n/a                 | number of affected tests in the current account group                                                                 |
| dateAffected            | dateTime          | yyyy-MM-dd hh:mm:ss | reflects the start date/time of the 5-minute interval when the location was recognized as affected, expressed in UTC. |
| locationId              | integer           | n/a                 | numeric location identifier. The number is chosen internally for each location by ThousandEyes, and will not change   |
| locationName            | string            | n/a                 | textual location identifier                                                                                           |
| permalink               | string            | n/a                 | hyperlink to alerts list, with row expanded                                                                           |

Monitor objects (available for `bgp` alert type only, see above) reflect the following content:

| Field          | Data Type | Units               | Notes                                                                                                                                                                                                                                             |
| -------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| asName         | string    | n/a                 | name of the monitor???s home Autonomous System                                                                                                                                                                                                      |
| asn            | integer   | n/a                 | number of the monitor???s home Autonomous System                                                                                                                                                                                                    |
| dateEnd        | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the earlier of the date that the alert was cleared, or the source reported a measurement that was under the alert rule???s threshold, expressed in UTC                                                                                     |
| dateStart      | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the date that the source began reporting a measurement that exceeded the alert rule???s threshold, expressed in UTC                                                                                                                        |
| metricsAtEnd   | string    | n/a                 | string representation of the metric or metrics being considered in the alert rule at the point that the alert was cleared. If the alert is not yet cleared, this field reflects the last round of data gathered from the source.                  |
| metricsAtStart | string    | n/a                 | string representation of the metric at the time that the source began alerting. Note that the alert start and dateStart for a particular source do not need to be the same, as sources may change alerting status throughout an alert???s lifecycle |
| monitorId      | integer   | n/a                 | unique ID of monitor violating the alert rule. See `/bgp-monitors` for more detail                                                                                                                                                                |
| monitorName    | string    | n/a                 | display name of the monitor violating the alert rule                                                                                                                                                                                              |
| permalink      | string    | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                                       |
| prefix         | string    | n/a                 | network prefix affected, expressed as `a.b.c.d/e` (or IPv6 equivalent)                                                                                                                                                                            |
| prefixId       | integer   | n/a                 | numeric prefix identifier. The number is chosen internally for each prefix by ThousandEyes, and will not change                                                                                                                                   |
| state          | string    | n/a                 | current state of the alert for this monitor. Possible values: `ACTIVE`, `CLEARED`, or `DISABLED` (when the test is deleted or disabled, or when the alert rule is deleted or disassociated from the test)                                         |

Location objects (available for `application-outage` alert type only, see above) reflect the following content:

| Field                | Data Type         | Units               | Notes                                                                                                                 |
| -------------------- | ----------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| affectedServersCount | integer           | n/a                 | number of servers affected by this outage                                                                             |
| affectedTests        | array of integers | n/a                 | array of affected `testId`s in the current account group                                                              |
| affectedTestsCount   | integer           | n/a                 | number of affected tests in the current account group                                                                 |
| dateAffected         | dateTime          | yyyy-MM-dd hh:mm:ss | reflects the start date/time of the 5-minute interval when the location was recognized as affected, expressed in UTC. |
| locationId           | integer           | n/a                 | numeric location identifier. The number is chosen internally for each location by ThousandEyes, and will not change   |
| locationName         | string            | n/a                 | textual location identifier                                                                                           |
| permalink            | string            | n/a                 | hyperlink to alerts list, with row expanded                                                                           |

`HTTP/1.1 200 OK Date: Thu, 23 Apr 2020 13:09:28 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1587647400 Strict-Transport-Security: max-age=31536000`

**Body - with agents**

`{ "agents": [ { "agentId": 813, "dateEnd": "2020-04-23 13:44:18", "dateStart": "2020-04-23 13:43:16", "metricsAtEnd": "Error: \"\"", "metricsAtStart": "Error: \"500 Internal Server Error\"", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=7625&alertId=2556232&agentId=813", "state": "CLEARED" }, ... ], "alertId": 2556232, "alertType": "http-server", "apiLinks": [ { "href": "https://api.thousandeyes.com/v7/alerts/http-server/2556232", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/alert-rules/289585.json", "rel": "rule" }, { "href": "https://api.thousandeyes.com/v6/tests/83126.json", "rel": "related" }, { "href": "https://api.thousandeyes.com/v6/web/http-server/83126.json", "rel": "data" } ], "dateEnd": "2020-04-23 13:44:18", "dateStart": "2020-04-23 13:43:16", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=7625&alertId=2556232", "ruleId": 289585, "state": "CLEARED", "testId": 83126, "violationCount": 1, "severity": "INFO" }`

**Body - with network outage locations**

`{ "alertId": 2542187, "alertType": "network-outage", "apiLinks": [ { "href": "https://api.thousandeyes.com/v7/alerts/network-outage/2542187", "rel": "self" } ], "asName": "Level 3 Communications, Inc.", "asn": 3356, "dateStart": "2020-04-13 16:20:00", "locations": [ { "affectedInterfacesCount": 2, "affectedTests": [ 12123 ], "affectedTestsCount": 1, "dateAffected": "2020-04-13 16:20:00", "locationId": 2925533, "locationName": "Frankfurt am Main, Germany", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=2542187&locationId=2925533" }, { "affectedInterfacesCount": 1, "affectedTests": [ 12123 ], "affectedTestsCount": 1, "dateAffected": "2020-04-13 16:20:00", "locationId": 4180439, "locationName": "Atlanta, Georgia, US", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=2542187&locationId=4180439" }, ... ], "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=2542187", "ruleId": 289901, "state": "ACTIVE", "severity": "INFO" }`

**Body - with BGP monitors**

`{ "alertId": 314935, "alertType": "bgp", "apiLinks": [ { "href": "https://api.thousandeyes.com/v7/alerts/bgp/314935", "rel": "self" }, ... ], "dateStart": "2017-10-06 18:15:00", "monitors": [ { "asName": "Elisa Oyj", "asn": 6667, "dateStart": "2018-08-26 18:00:00", "metricsAtEnd": "", "metricsAtStart": "Reachability: 99.8%", "monitorId": 53, "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=314935&monitorId=53", "prefix": "93.168.254.0/23", "prefixId": 610088, "state": "ACTIVE" }, { "asName": "ColocationIX GmbH", "asn": 61955, "dateStart": "2020-04-07 17:15:00", "metricsAtEnd": "", "metricsAtStart": "Reachability: 0%", "monitorId": 4131, "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=314935&monitorId=4131", "prefix": "93.168.254.0/23", "prefixId": 610088, "state": "ACTIVE" }, ... ], "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=314935", "ruleId": 75409, "state": "ACTIVE", "testId": 25611, "violationCount": 86, "severity": "INFO" }`

**Body - with application outage locations**

`{ "alertId": 35085, "alertType": "application-outage", "apiLinks": [ { "href": "https://api.thousandeyes.com/v7/alerts/application-outage/35085", "rel": "self" } ], "applicationName": "Paypal", "dateStart": "2020-04-13 16:20:00", "locations": [ { "affectedServersCount": 2, "affectedTests": [ 12123 ], "affectedTestsCount": 1, "dateAffected": "2020-04-13 16:20:00", "locationId": 2925533, "locationName": "Frankfurt am Main, Germany", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=35085&locationId=2925533" }, { "affectedServersCount": 1, "affectedTests": [ 12123 ], "affectedTestsCount": 1, "dateAffected": "2020-04-13 16:20:00", "locationId": 4180439, "locationName": "Atlanta, Georgia, US", "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=35085&locationId=4180439" }, ... ], "permalink": "https://app.thousandeyes.com/alerts/list/?__a=11&alertId=35085", "ruleId": 2021, "state": "ACTIVE", "severity": "INFO" }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).
