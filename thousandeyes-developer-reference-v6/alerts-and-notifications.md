# Alerts & Notifications

### Alerts & Notifications

[`GET /v6/alerts` Active alerts](broken-reference)

Returns a list of all active alerts, active at any given time.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alerts.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of active alerts, either at present, or based on the time range specified, indicating testId and testName, alert rule. If no alerts are active during the time range specified, an empty response will be returned.

| Field          | Data Type                | Units               | Notes                                                                                                                                                                                                                                  |
| -------------- | ------------------------ | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertId        | integer                  | n/a                 | unique ID of the alert; each alert occurrence is assigned a new unique ID                                                                                                                                                              |
| testId         | integer                  | n/a                 | unique ID of the test (see `/tests/{testId}` endpoint for more detail)                                                                                                                                                                 |
| ruleId         | integer                  | n/a                 | unique ID of the alert rule (see `/alert-rules` endpoint for more detail)                                                                                                                                                              |
| testName       | string                   | n/a                 | name of the test                                                                                                                                                                                                                       |
| active         | integer                  | n/a                 | 0 for inactive, 1 for active, 2 for disabled. Alert is disabled if either alert rule itself has been deleted or the test it is applied to has been disabled, deleted, disabled alerting, or disassociated the alert rule from the test |
| ruleExpression | string                   | n/a                 | string expression of alert rule                                                                                                                                                                                                        |
| dateStart      | dateTime                 | yyyy-MM-dd hh:mm:ss | the date/time where an alert rule was triggered, expressed in UTC                                                                                                                                                                      |
| dateEnd        | dateTime                 | yyyy-MM-dd hh:mm:ss | the date/time where the alert was marked as cleared, expressed in UTC                                                                                                                                                                  |
| violationCount | integer                  | n/a                 | number of sources currently meeting the alert criteria                                                                                                                                                                                 |
| ruleName       | string                   | n/a                 | name of the alert rule                                                                                                                                                                                                                 |
| permalink      | string                   | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                            |
| type           | string                   | n/a                 | type of alert being triggered                                                                                                                                                                                                          |
| agents         | array of agent objects   | n/a                 | array of monitors where the alert has at some point been active since the point that the alert was triggered. Not shown on BGP alerts.                                                                                                 |
| monitors       | array of monitor objects | n/a                 | array of monitors where the alert has at some point been active since the point that the alert was triggered. Only shown on BGP alerts.                                                                                                |
| apiLinks       | array of links           | n/a                 | list of hyperlinks to other areas of the API                                                                                                                                                                                           |
| severity       | string                   | n/a                 | field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                                                               |

Agent and Monitor objects (see above) reflect the following content:

| Field                 | Data Type | Units               | Notes                                                                                                                                                                                                                                                |
| --------------------- | --------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dateStart             | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the date that the source began reporting a measurement that exceeded the alert rule’s threshold, expressed in UTC                                                                                                                           |
| dateEnd               | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the earlier of the date that the alert was cleared, or the source reported a measurement that was under the alert rule’s threshold, expressed in UTC                                                                                        |
| active                | boolean   | n/a                 | if the particular source is alerting when the API is queried, this flag will be set to 1. After an alert has cleared, this flag (regardless of the source’s metrics) will be set to 0, even if the particular source has not cleared the alert rule. |
| metricsAtStart        | string    | n/a                 | string representation of the metric at the time that the source began alerting. Note that the alert start and dateStart for a particular source do not need to be the same, as sources may change alerting status throughout an alert’s lifecycle    |
| metricsAtEnd          | string    | n/a                 | string representation of the metric or metrics being considered in the alert rule at the point that the alert was cleared. If the alert is not yet cleared, this field reflects the last round of data gathered from the source.                     |
| agentId/monitorId     | integer   | n/a                 | unique ID of agent or monitor violating the alert rule. See `/agents` or `/bgp-monitors` for more detail                                                                                                                                             |
| agentName/monitorName | string    | n/a                 | display name of the agent or monitor violating the alert rule                                                                                                                                                                                        |
| permalink             | string    | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                                          |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493373360 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-1`

**Body**

`{ "alert": [ { "alertId": 2783, "testId": 822, "ruleId": 142, "testName": "thousandeyes.com A", "active": 1, "ruleExpression": "((probDetail != \"\"))", "dateStart": "2012-12-13 13:15:00", "violationCount": 6, "ruleName": "Default DNSSEC Alert Rule", "createLinks": true, "permalink": "https://app.thousandeyes.com/alerts/list?__a=75&alertId=2783", "type": "DNSSEC", "agents": [ { "agentId": 12, "agentName": "Hong Kong", "dateStart": "2012-12-13 13:15:00", "active": 1, "metricsAtStart": "Error details: \"No DNSSEC public key(s) for thousandeyes.com A\"", "metricsAtEnd": "Error details: \"No DNSSEC public key(s) for thousandeyes.com A\"", "permalink": "https://app.thousandeyes.com/alerts/list?__a=75&alertId=2783&agentId=12" }, ... ], "apiLinks": [...], "severity": "INFO" } ], "pages": { "current": 1 } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/alerts/{alertId}` Alert detail](broken-reference)

Returns details about an alert.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alerts/34203.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed information about a specific alertId. If the alertId doesn’t exist or is inaccessible by your account, an empty response will be returned.

| Field          | Data Type                | Units               | Notes                                                                                                                                                                                                                                  |
| -------------- | ------------------------ | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ruleId         | integer                  | n/a                 | unique ID of the alert rule (see `/alert-rules` endpoint for more detail)                                                                                                                                                              |
| alertId        | integer                  | n/a                 | unique ID of the alert; each alert occurrence is assigned a new unique ID                                                                                                                                                              |
| testId         | integer                  | n/a                 | unique ID of the test (see `/tests/{testId}` endpoint for more detail)                                                                                                                                                                 |
| testName       | string                   | n/a                 | name of the test                                                                                                                                                                                                                       |
| active         | integer                  | n/a                 | 0 for inactive, 1 for active, 2 for disabled. Alert is disabled if either alert rule itself has been deleted or the test it is applied to has been disabled, deleted, disabled alerting, or disassociated the alert rule from the test |
| ruleExpression | string                   | n/a                 | string expression of alert rule                                                                                                                                                                                                        |
| dateStart      | dateTime                 | yyyy-MM-dd hh:mm:ss | the date/time where an alert rule was triggered, expressed in UTC                                                                                                                                                                      |
| dateEnd        | dateTime                 | yyyy-MM-dd hh:mm:ss | the date/time where the alert was marked as cleared, expressed in UTC                                                                                                                                                                  |
| violationCount | integer                  | n/a                 | number of sources currently meeting the alert criteria                                                                                                                                                                                 |
| ruleName       | string                   | n/a                 | name of the alert rule                                                                                                                                                                                                                 |
| permalink      | string                   | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                            |
| type           | string                   | n/a                 | type of alert being triggered                                                                                                                                                                                                          |
| agents         | array of agent objects   | n/a                 | array of agents where the alert has at some point been active since the point that the alert was triggered. Not shown on BGP alerts.                                                                                                   |
| monitors       | array of monitor objects | n/a                 | array of monitors where the alert has at some point been active since the point that the alert was triggered. Only shown on BGP alerts.                                                                                                |
| apiLinks       | array of links           | n/a                 | list of hyperlinks to other areas of the API                                                                                                                                                                                           |
| severity       | string                   | n/a                 | field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                                                               |

Agent and Monitor objects (see above) reflect the following content:

| Field                 | Data Type | Units               | Notes                                                                                                                                                                                                                                                |
| --------------------- | --------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dateStart             | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the date that the source began reporting a measurement that exceeded the alert rule’s threshold, expressed in UTC                                                                                                                           |
| dateEnd               | dateTime  | yyyy-MM-dd hh:mm:ss | reflects the earlier of the date that the alert was cleared, or the source reported a measurement that was under the alert rule’s threshold, expressed in UTC                                                                                        |
| active                | boolean   | n/a                 | if the particular source is alerting when the API is queried, this flag will be set to 1. After an alert has cleared, this flag (regardless of the source’s metrics) will be set to 0, even if the particular source has not cleared the alert rule. |
| metricsAtStart        | string    | n/a                 | string representation of the metric at the time that the source began alerting. Note that the alert start and dateStart for a particular source do not need to be the same, as sources may change alerting status throughout an alert’s lifecycle    |
| metricsAtEnd          | string    | n/a                 | string representation of the metric or metrics being considered in the alert rule at the point that the alert was cleared. If the alert is not yet cleared, this field reflects the last round of data gathered from the source.                     |
| agentId/monitorId     | integer   | n/a                 | unique ID of agent or monitor violating the alert rule. See `/agents` or `/bgp-monitors` for more detail                                                                                                                                             |
| agentName/monitorName | string    | n/a                 | display name of the agent or monitor violating the alert rule                                                                                                                                                                                        |
| permalink             | string    | n/a                 | hyperlink to alerts list, with row expanded                                                                                                                                                                                                          |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493373360 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-1`

**Body**

`{ "alert": [ { "ruleId": 172, "alertId": 34203, "testId": 5176, "testName": "API created test", "active": 1, "ruleExpression": "((errorType != \"None\"))", "dateStart": "2014-03-24 19:02:00", "violationCount": 2, "ruleName": "Default HTTP Alert Rule", "permalink": "https://app.thousandeyes.com/alerts/list?__a=11&alertId=32403", "type": "HTTP Server", "agents": [ { "dateStart": "2014-03-24 19:02:00", "active": 1, "metricsAtStart": "Error type: \"DNS\"", "metricsAtEnd": "Error type: \"DNS\"", "agentId": 107, "agentName": "Vancouver, Canada", "permalink": "https://app.thousandeyes.com/web/http-server?__a=11&testId=5176&roundId=1395699129&agentId=107" }, { "dateStart": "2014-03-24 19:01:48", "active": 1, "metricsAtStart": "Error type: \"DNS\"", "metricsAtEnd": "Error type: \"DNS\"", "agentId": 108, "agentName": "Boston, MA", "permalink": "https://app.thousandeyes.com/web/http-server?__a=11&testId=5176&roundId=1395699129&agentId=108" } ], "apiLinks": [...], "severity": "INFO" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/alert-rules` Alert rules](broken-reference)

Returns a list of all alert rules configured under your account in ThousandEyes.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alert-rules.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of alert rules, indicating ruleID, whether or not the alert is enabled, recipient lists, and the rule criteria and clearing logic. Default rules for each type are indicated with a bit response (1 or 0); default alert rules are assigned by default to each type of test to which they apply.

| Field                   | Data Type | Units | Notes                                                                                                                                                                                                                                 |
| ----------------------- | --------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ruleId                  | integer   | n/a   | unique ID of the alert rule                                                                                                                                                                                                           |
| ruleName                | string    | n/a   | name of the alert rule                                                                                                                                                                                                                |
| expression              | string    | n/a   | string expression of alert rule                                                                                                                                                                                                       |
| direction               | string    | n/a   | optional field with one of the following values: `TO_TARGET`, `FROM_TARGET`, `BIDIRECTIONAL`, for applicable alert types (eg. path trace, End-to-End (Agent) etc.)                                                                    |
| notifyOnClear           | boolean   | n/a   | 1 to send notification when alert clears                                                                                                                                                                                              |
| default                 | boolean   | n/a   | Alert rules allow up to 1 alert rule to be selected as a default for each type. By checking the default option, this alert rule will be automatically included on subsequently created tests that test a metric used in alerting here |
| alertType               | string    | n/a   | type of alert rule, as determined by metric selection                                                                                                                                                                                 |
| minimumSources          | integer   | n/a   | the minimum number of agents or monitors that must meet the specified criteria in order to trigger the alert                                                                                                                          |
| minimumSourcesPct       | integer   | n/a   | the minimum percentage of all assigned agents or monitors that must meet the specified criteria in order to trigger the alert                                                                                                         |
| roundsViolatingMode     | string    | n/a   | `EXACT` requires that the same agent(s) meet the threshold in consecutive rounds; default is `ANY`                                                                                                                                    |
| roundsViolatingOutOf    | integer   | n/a   | applies to only v6 and higher, specifies the divisor (y value) for the “X of Y times” condition.                                                                                                                                      |
| roundsViolatingRequired | integer   | n/a   | applies to only v6 and higher, specifies the numerator (x value) for the “X of Y times” condition                                                                                                                                     |
| severity                | string    | n/a   | field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                                                              |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493373360 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-1`

**Body**

`{ "alertRules": [ { "alertType": "Path Trace", "default": 0, "expression": "((hops((hopDelay >= 100 ms))))", "minimumSources": 1, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 9, "ruleId": 99453, "ruleName": "The End of the Internet", "severity": "INFO" }, { "alertType": "HTTP Server", "default": 0, "expression": "((errorType != \"None\"))", "minimumSourcesPct": 30, "notifyOnClear": 1, "roundsViolatingOutOf": 1, "roundsViolatingRequired": 1, "ruleId": 127094, "ruleName": "The End of the World", "severity": "CRITICAL" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/alert-rules/{ruleId}` Alert rule detail](broken-reference)

Returns details about an alert rule.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alert-rules/322.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed information about a specific alert rule. If the ruleId doesn’t exist or is inaccessible by your account, an empty response will be returned.

| Field                   | Data Type                           | Units | Notes                                                                                                                                                                                                                                 |
| ----------------------- | ----------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ruleId                  | integer                             | n/a   | unique ID of the alert rule                                                                                                                                                                                                           |
| ruleName                | string                              | n/a   | name of the alert rule                                                                                                                                                                                                                |
| expression              | string                              | n/a   | string expression of alert rule                                                                                                                                                                                                       |
| direction               | string                              | n/a   | optional field with one of the following values: `TO_TARGET`, `FROM_TARGET`, `BIDIRECTIONAL`, for applicable alert types (eg. path trace, End-to-End (Agent) etc.)                                                                    |
| notifications           | object with notification properties | n/a   | Alert notification object. See [Alert notification integrations](broken-reference).                                                                                                                                                   |
| notifyOnClear           | boolean                             | n/a   | 1 to send notification when alert clears                                                                                                                                                                                              |
| default                 | boolean                             | n/a   | Alert rules allow up to 1 alert rule to be selected as a default for each type. By checking the default option, this alert rule will be automatically included on subsequently created tests that test a metric used in alerting here |
| alertType               | string                              | n/a   | type of alert rule, as determined by metric selection                                                                                                                                                                                 |
| minimumSources          | integer                             | n/a   | the minimum number of agents or monitors that must meet the specified criteria in order to trigger the alert                                                                                                                          |
| minimumSourcesPct       | integer                             | n/a   | the minimum percentage of all assigned agents or monitors that must meet the specified criteria in order to trigger the alert                                                                                                         |
| roundsViolatingMode     | string                              | n/a   | `EXACT` requires that the same agent(s) meet the threshold in consecutive rounds; default is `ANY`                                                                                                                                    |
| roundsViolatingOutOf    | integer                             | n/a   | applies to only v6 and higher, specifies the divisor (y value) for the “X of Y times” condition.                                                                                                                                      |
| roundsViolatingRequired | integer                             | n/a   | applies to only v6 and higher, specifies the numerator (x value) for the “X of Y times” condition                                                                                                                                     |
| tests                   | array                               | n/a   | list of tests alert rule is assigned to, expressed in the same format as `/tests` endpoint                                                                                                                                            |
| severity                | string                              | n/a   | field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                                                              |

If Alert Rule has email notifications configured, `notifications` object has an `email` parameter. Email object has the following parameters:

| Field Name | Data Type                | Notes                                                                |
| ---------- | ------------------------ | -------------------------------------------------------------------- |
| recipient  | array of email addresses | notification recipients are specified in an array of email addresses |
| message    | string                   | additional content sent to notification recipients in alert emails   |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493373360 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-1`

**Body**

`{ "alertRules": [ { "ruleId": 322, "ruleName": "Default BGP Alert Rule", "notes": "", "expression": "((reachability < 100%))", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "channel": "@primoz", "integrationId": "sl-57", "integrationName": "Slack to Primoz", "integrationType": "SLACK", "target": "https://hooks.slack.com/services/T0DXA4R8U/B2Y23HERL/uL3lz43raw1HfakeIDRChoOH" }, { "authMethod": "Auth Token", "authToken": "a2b93fakeToken39feacf5fea49defacdc", "authUser": "thousandeyes", "integrationId": 1234, "integrationName": "Frontend ThousandEyes", "integrationType": "PAGER_DUTY" } ] }, "notifyOnClear": 0, "roundsBeforeTrigger": 1, "default": 1, "recipient": [], "alertType": "BGP", "tests": [ { "alertsEnabled": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "contentRegex": "", "createdBy": "Primoz (noreply@thousandeyes.com)", "createdDate": "2016-12-14 19:18:51", "enabled": 1, "followRedirects": 1, "httpInterval": 120, "httpTargetTime": 1000, "httpTimeLimit": 5, "includeHeaders": 0, "interval": 300, "liveShare": 0, "modifiedBy": "Primoz (noreply@thousandeyes.com)", "modifiedDate": "2017-04-07 11:08:47", "mtuMeasurements": 0, "networkMeasurements": 1, "pageLoadTargetTime": 6, "pageLoadTimeLimit": 10, "savedEvent": 0, "sslVersion": "Auto", "sslVersionId": 0, "testId": 35180, "testName": "Google PL", "type": "page-load", "url": "http://google.com", "useNtlm": 0, "verifyCertificate": 1 } ], "severity": "INFO" }, { "ruleId": 300, "ruleName": "Default DNS Server Alert Rule", "notes": "", "expression": "((probDetail != \"\"))", "minimumSources": 2, "notifyOnClear": 0, "roundsBeforeTrigger": 1, "default": 1, "recipient": [ "noreply@thousandeyes.com" ], "alertType": "DNS Server", "severity": "MAJOR" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[Alert rule metadata](broken-reference)

Alert rule fields are shown in the table below. The table indicates whether the fields can rule creation, updates, or simply in returning data. As a reminder, in order to create a new alert rule, the user attempting the creation must be in a role which includes the Edit Alert rules permission.

Fields are listed in the table below.

Where a field indicates n/a for both Alert rule creation and update, these fields are system-generated and read only, and displayed as part of test metadata.

| Field                   | Creation   | Update     | Data Type                           | Accepts                                                                                                                                       | Notes/Example                                                                                                                                                                                                                                                                                                           |
| ----------------------- | ---------- | ---------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertType               | required   | required   | string                              | Acceptable test types, verbose names.                                                                                                         | Page Load, HTTP Server, End-to-End (Server), End-to-End (Agent), Voice, DNS Server, DNS Trace, DNSSEC, Web Transactions, BGP, Path Trace, FTP, SIP Server                                                                                                                                                               |
| ruleName                | required   | required   | string                              | name of the alert rule                                                                                                                        | the name of the alert rule                                                                                                                                                                                                                                                                                              |
| default                 | optional   | optional   | bit                                 | to set the rule as a default, set this value to 1.                                                                                            | Defaults to 0                                                                                                                                                                                                                                                                                                           |
| expression              | required   | required   | string                              | Expression string should be a valid JSON string.                                                                                              | See examples in the table below. Use examples found on the Alert Rule Detail endpoint.                                                                                                                                                                                                                                  |
| notifications           | optional   | optional   | object with notification properties | See notifications endpoint for examples                                                                                                       | `"notifications": { "email": { "message": "NA", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" }, {"integrationId": "pgd-21","integrationType": "PAGER_DUTY"} ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] },` |
| notifyOnClear           | optional   | optional   | bit                                 | set to 1 to trigger the notification when the alert clears.                                                                                   | Defaults to 0.                                                                                                                                                                                                                                                                                                          |
| testIds                 | optional   | optional   | array of integers                   | valid test Ids                                                                                                                                | `"testIds": [12345, 12346]`                                                                                                                                                                                                                                                                                             |
| minimumSources          | optional\* | optional\* | integer                             | The minimum number of agents or monitors that must meet the specified criteria in order to trigger an alert                                   | Either minimumSources or minimumSourcesPct must be specified in create calls                                                                                                                                                                                                                                            |
| minimumSourcesPct       | optional\* | optional\* | integer                             | The minimum percentage of agents or monitors that must meet the specified criteria in order to trigger an alert                               | Either minimumSources or minimumSourcesPct must be specified in create calls                                                                                                                                                                                                                                            |
| roundsViolatingMode     | optional   | optional   | string                              | `ANY` or `EXACT`                                                                                                                              | `EXACT` requires that the same agent(s) meet the threshold in consecutive rounds; default is `ANY`                                                                                                                                                                                                                      |
| roundsViolatingRequired | required   | required   | Integer                             | specifies the numerator (X value) of the “X of Y times” condition in an alert rule.                                                           | Minimum value is 1, maximum value is 10. Must be less than or equal to `roundsViolatingOutOf`                                                                                                                                                                                                                           |
| roundsViolatingOutOf    | required   | required   | Integer                             | specifies the divisor (Y value) of the “X of Y times” condition in an alert rule.                                                             | Minimum value is 1, maximum value is 10.                                                                                                                                                                                                                                                                                |
| direction               | optional   | optional   | string                              | For alertTypes `End-to-end (Agent)` and `Path Trace`, field must be set to a value from this list: \[TO\_TARGET, FROM\_TARGET, BIDIRECTIONAL] | see accepts section                                                                                                                                                                                                                                                                                                     |
| includeCoveredPrefixes  | optional   | optional   | bit                                 | set to 1 to include covered prefixes in the BGP alert rule. Only applicable to BGP alert rules                                                | Defaults to 1                                                                                                                                                                                                                                                                                                           |
| severity                | optional   | optional   | string                              | valid severity string                                                                                                                         | optional field with one of the following values: INFO, MAJOR, MINOR, CRITICAL for all alert types                                                                                                                                                                                                                       |

### Expressions <a href="#expressions" id="expressions"></a>

The following table outlines a list of expressions that can be used when creating or modifying alert rules. Multiple metrics can be combined in a single rule with logical “and” and logical “or” operators, using double-ampersand (`&&`) and double-pipe (`||`), respectively. When combining three or more metrics, a single operator type is allowed, i.e. both logical “and” and logical “or” operators cannot be used. Note that not all metrics can be combined into a single rule.

For more information on metrics please refer to [How alerts work](https://docs.thousandeyes.com/product-documentation/alerts/how-alerts-work) for more information on supported metrics.

| Alert type       | Metric                       | Operator                | Data type                                                                                                                                | Example                                                               | Notes                                                                                                                                                                                                |
| ---------------- | ---------------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTP Server      | responseCode                 | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((responseCode >= 400))`                                             | HTTP response code returned by the test                                                                                                                                                              |
| HTTP Server      | dnsTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((dnsTime >= 500 ms))`                                               | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | connectTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((connectTime >= 500 ms))`                                           | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | sslTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((sslTime >= 500 ms))`                                               | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | waitTime                     | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((waitTime >= 500 ms))`                                              | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | receiveTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((receiveTime >= 500 ms))`                                           | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | totalTime                    | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((totalTime >= 500 ms))`                                             | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | responseTime                 | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((responseTime >= 500 ms))`                                          | ensure that you set units in the expression                                                                                                                                                          |
| HTTP Server      | errorType                    | \[=, !=]                | \[None, SSL, DNS, Connect]                                                                                                               | `((errorType != "None"))`                                             | errorType is specified as a string from list of valid error types. Double-quote enclose.                                                                                                             |
| HTTP Server      | clientSslAlertCode           | \[==, !=]               | Integer                                                                                                                                  | `((clientSslAlertCode != 40))`                                        | SSL error code                                                                                                                                                                                       |
| HTTP Server      | serverSslAlertCode           | \[==, !=]               | Integer                                                                                                                                  | `((serverSslAlertCode != 40))`                                        | SSL error code                                                                                                                                                                                       |
| HTTP Server      | throughput                   | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((throughput >= 100 kbps))`                                          | ensure that you set units in the expression.                                                                                                                                                         |
| HTTP Server      | responseHeaders              | \[=\~, !\~]             | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((responseHeaders =~ /"\\wFoo\//))`                                  | Text match for response headers                                                                                                                                                                      |
| HTTP Server      | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /google/))`                                          | Problem detail (???)                                                                                                                                                                                 |
| HTTP Server      | redirectCount                | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((redirectCount >= 2))`                                              | Number of redirects from the target page                                                                                                                                                             |
| HTTP Server      | wireSize                     | \[<, <=, ==, !=, >=, >] | Float                                                                                                                                    | `((wireSize > 1024.0 kB))`                                            | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | ftpReplyCode                 | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((ftpReplyCode >= 400))`                                             | FTP reply code                                                                                                                                                                                       |
| FTP Server       | dnsTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((dnsTime >= 500 ms))`                                               | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | connectTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((connectTime >= 500 ms))`                                           | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | sslTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((sslTime >= 500 ms))`                                               | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | negotiationTime              | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((negotiationTime >= 500 ms))`                                       | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | waitTime                     | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((waitTime >= 500 ms))`                                              | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | transferTime                 | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((transferTime >= 500 ms))`                                          | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | totalTime                    | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((totalTime >= 500 ms))`                                             | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | responseTime                 | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((responseTime >= 500 ms))`                                          | ensure that you set units in the expression                                                                                                                                                          |
| FTP Server       | ftpErrorType                 | \[=, !=]                | \[None, SSL, DNS, Connect]                                                                                                               | `((ftpErrorType != "None"))`                                          | errorType is specified as a string from list of valid error types. Double-quote enclose.                                                                                                             |
| FTP Server       | throughput                   | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((throughput >= 100 kbps))`                                          | ensure that you set units in the expression.                                                                                                                                                         |
| Network          | loss                         | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((loss >= 10%))`                                                     | set loss threshold in percent                                                                                                                                                                        |
| Network          | avgLatency                   | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((avgLatency >= 100 ms))`                                            | ensure that you set units in the expression                                                                                                                                                          |
| Network          | jitter                       | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((jitter >= 15 ms))`                                                 | ensure that you set units in expression                                                                                                                                                              |
| Network          | availBwCs                    | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((availBwCs >= 10 Mbps))`                                            | ensure that you set units in expression                                                                                                                                                              |
| Network          | capCs                        | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((capCs >= 10 Mbps))`                                                | ensure that you set units in expression                                                                                                                                                              |
| All              | locationId                   | \[in, !in]              | list                                                                                                                                     | `[(locationId !in {"1", "2"})`]                                       | locationId reflects the agentId for agent-based tests, and monitorId for BGP-based tests                                                                                                             |
| Page Load        | pageLoaded                   | n/a                     | n/a                                                                                                                                      | `((!pageLoaded))`                                                     | use !pageLoaded to trigger an alert when the page doesn’t load                                                                                                                                       |
| Page Load        | pageLoadHasError             | \[\\==]                 | boolean                                                                                                                                  | `((pageLoadHasError == true))`                                        | fire when the page load has a component error                                                                                                                                                        |
| Page Load        | pageLoadTimedOut             | \[==]                   | boolean                                                                                                                                  | `((pageLoadTimedOut == true))`                                        | fire when page load times out                                                                                                                                                                        |
| Page Load        | timeToFirstByte              | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((timeToFirstByte >= 100 ms))`                                       | ensure that you set units in the expression                                                                                                                                                          |
| Page Load        | onContentLoadTime            | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((onContentLoadTime >= 100 ms))`                                     | ensure that you set units in the expression. This reflects the DOM Load value in the page load.                                                                                                      |
| Page Load        | onLoadTime                   | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((onLoadTime >= 100 ms))`                                            | ensure that you set units in the expression. This metric reflects page load time.                                                                                                                    |
| Page Load        | errorCount                   | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((errorCount >= 2))`                                                 | number of component errors                                                                                                                                                                           |
| Page Load        | components                   | see notes               | see notes                                                                                                                                | see notes                                                             | wrap component-specific criteria in a set of parentheses                                                                                                                                             |
| Page Load        | domain                       | \[in, !in]              | list of strings                                                                                                                          | `((components((domain !in {"*.facebook.com"}))))`                     | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | totalTime                    | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((totalTime >= 100 ms))))`                               | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | blockedTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((totalTime >= 100 ms))))`                               | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | dnsTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((dnsTime >= 100 ms))))`                                 | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | connectTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((connectTime >= 100 ms))))`                             | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | waitTime                     | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((waitTime >= 100 ms))))`                                | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | receiveTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((receiveTime >= 100 ms))))`                             | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | sslTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((components((sslTime >= 100 ms))))`                                 | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | componentLoaded              | \[==, !=]               | bit                                                                                                                                      | `((components((componentLoaded == 0))))`                              | must be wrapped by components(), applies at the component level                                                                                                                                      |
| Page Load        | wireSize                     | \[<, <=, ==, !=, >=, >] | float + units                                                                                                                            | `((wireSize > 1024.0 kB))`                                            | ensure you set units as part of the expression                                                                                                                                                       |
| Web Transactions | assertError                  | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((assertError =~ /foo/))`                                            | Assert Error                                                                                                                                                                                         |
| Web Transactions | duration                     | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((duration >= 100 ms))`                                              | ensure you set units as part of the expression                                                                                                                                                       |
| Web Transactions | markerDuration               | \[<, <=, ==, !=, >=, >] | String + Integer + units                                                                                                                 | `((marker[((markerName == "Marker1"))]((markerDuration >= 100 ms))))` | ensure you set units as part of the expression                                                                                                                                                       |
| Web Transactions | onContentLoadTime            | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((webPages((onContentLoadTime <= 100 ms))))`                         | DOM load time. Ensure you set units as part of the expression                                                                                                                                        |
| Web Transactions | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem details                                                                                                                                                                                      |
| Web Transactions | txCompletionFinished         | \[==]                   | boolean                                                                                                                                  | `((txCompletionFinished == true))`                                    | Transaction completed                                                                                                                                                                                |
| Web Transactions | txCompletionHasError         | \[==]                   | boolean                                                                                                                                  | `((txCompletionHasError == true))`                                    | Transaction completed with errors                                                                                                                                                                    |
| Web Transactions | txCompletionHasInternalError | \[==]                   | boolean                                                                                                                                  | `((txCompletionHasInternalError == true))`                            | Transaction completed with internal errors                                                                                                                                                           |
| Web Transactions | txCompletionTimedOut         | \[==]                   | boolean                                                                                                                                  | `((txCompletionTimedOut == true))`                                    | Transaction completed due to reaching timeout value                                                                                                                                                  |
| Web Transactions | webTxOnLoadTime              | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((webPages((webTxOnLoadTime >= 100 ms))))`                           | Page load time. Ensure that you set units in the expression                                                                                                                                          |
| Web Transactions | webTxResponseTime            | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((webPages((webTxResponseTime >= 100 ms))))`                         | Response time. Ensure that you set units in the expression                                                                                                                                           |
| Web Transactions | webTxPageLoadError           | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((webPages((webTxPageLoadError =~ /foo/))))`                         | Page load error received                                                                                                                                                                             |
| DNS Server       | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem details                                                                                                                                                                                      |
| DNS Server       | delay                        | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((delay >= 100 ms))`                                                 | ensure you set units as part of the expression                                                                                                                                                       |
| DNS Server       | mapData                      | \[in, !in]              | list                                                                                                                                     | `((mapData !in {"10.0.0.0/8"}))`                                      | list can reflect IP addresses, CIDR blocks, or strings. Wildcards are supported for domains                                                                                                          |
| DNS Trace        | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem details                                                                                                                                                                                      |
| DNS Trace        | mapData                      | \[in, !in]              | list                                                                                                                                     | `((mapData !in {"10.0.0.0/8"}))`                                      | list can reflect IP addresses, CIDR blocks, or strings. Wildcards are supported for domains                                                                                                          |
| DNSSEC           | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem details                                                                                                                                                                                      |
| Voice            | mos                          | \[<, <=, ==, !=, >=, >] | Float                                                                                                                                    | `((mos >= 2.75))`                                                     | note: mean opinion scores do not have units                                                                                                                                                          |
| Voice            | loss                         | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((loss >= 10%))`                                                     | set loss threshold in percent                                                                                                                                                                        |
| Voice            | latency                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((latency >= 100 ms))`                                               | ensure that you set units in the expression                                                                                                                                                          |
| Voice            | pdv                          | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((pdv >= 15 ms))`                                                    | ensure that you set units in expression                                                                                                                                                              |
| Voice            | loss                         | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((loss >= 10%))`                                                     | set loss threshold in percent                                                                                                                                                                        |
| Voice            | discards                     | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((discards >= 10%))`                                                 | set discard threshold in percent                                                                                                                                                                     |
| Voice            | dscp                         | \[==, !=]               | Integer                                                                                                                                  | `((dscp != 26))`                                                      | set DSCP value received by target agent                                                                                                                                                              |
| Voice            | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem details                                                                                                                                                                                      |
| SIP Server       | sipResponseCode              | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((sipResponseCode >= 400))`                                          | reflects response code to SIP register                                                                                                                                                               |
| SIP Server       | sipErrorType                 | \[==, !=]               | string                                                                                                                                   | `((sipErrorType != "None"))`                                          | SIP error type (dns, connect, register, invite, options, none)                                                                                                                                       |
| SIP Server       | dnsTime                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((dnsTime >= 100 ms))`                                               | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | connectTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((connectTime >= 100 ms))`                                           | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | registerTime                 | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((registerTime >= 100 ms))`                                          | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | inviteTime                   | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((inviteTime >= 100 ms))`                                            | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | optionsTime                  | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((optionsTime >= 100 ms))`                                           | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | waitTime                     | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((waitTime >= 100 ms))`                                              | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | responseTime                 | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((responseTime >= 100 ms))`                                          | ensure you set units as part of the expression                                                                                                                                                       |
| SIP Server       | totalTime                    | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((totalTime >= 100 ms))`                                             | ensure you set units as part of the expression                                                                                                                                                       |
| Agent to Agent   | loss                         | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((loss >= 10%))`                                                     | set loss threshold in percent                                                                                                                                                                        |
| Agent to Agent   | latency                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((latency >= 100 ms))`                                               | ensure that you set units in the expression                                                                                                                                                          |
| Agent to Agent   | jitter                       | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((jitter >= 15 ms))`                                                 | ensure that you set units in expression                                                                                                                                                              |
| Agent to Agent   | throughput                   | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((throughput >= 10 Mbps))`                                           | ensure that you set units in expression                                                                                                                                                              |
| Agent to Agent   | probDetail                   | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem detail                                                                                                                                                                                       |
| Agent to Agent   | dscp                         | \[==, !=]               | Integer                                                                                                                                  | `((dscp != 26))`                                                      | set DSCP value received by target agent                                                                                                                                                              |
| Agent to Agent   | bothWaysLoss                 | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((bothWaysLoss >= 10%))`                                             | set loss threshold in percent                                                                                                                                                                        |
| Agent to Agent   | bothWaysLatency              | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((bothWaysLatency >= 100 ms))`                                       | ensure that you set units in the expression                                                                                                                                                          |
| Agent to Agent   | bothWaysJitter               | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((bothWaysJitter >= 15 ms))`                                         | ensure that you set units in expression                                                                                                                                                              |
| Agent to Agent   | bothWaysThroughput           | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((bothWaysThroughput >= 10 Mbps))`                                   | ensure that you set units in expression                                                                                                                                                              |
| Agent to Agent   | bothWaysProbDetail           | \[=\~, !=, !\~]         | [Regular expression](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | `((probDetail =~ /foo/))`                                             | Problem details                                                                                                                                                                                      |
| Path Trace       | serverIP                     | \[in, !in]              | list                                                                                                                                     | `((serverIp !in {"20.0.0.1", "10.0.0.0/8"}))`                         | IP address of target server                                                                                                                                                                          |
| Path Trace       | mss                          | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((mss >= 1460 B))`                                                   | ensure you set units as part of the expression                                                                                                                                                       |
| Path Trace       | pathMtu                      | \[<, <=, ==, !=, >=, >] | Integer + units                                                                                                                          | `((pathMtu >= 1500 B))`                                               | ensure you set units as part of the expression                                                                                                                                                       |
| Path Trace       | pathLength                   | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((pathLength >= 15))`                                                | total length of the path from source to target                                                                                                                                                       |
| Path Trace       | isTerminal                   | \[==]                   | Boolean                                                                                                                                  | `((isTerminal == true))`                                              | Value is set to true in the event that the path trace does not reach the destination                                                                                                                 |
| Path Trace       | hops                         | see notes               | see notes                                                                                                                                | see notes                                                             | wrap hop-specific criteria in a set of parentheses, use array position to indicate hop number. To test any hop, use hops without specifying an array. Use negative numbers to test hops from target. |
| Path Trace       | noHops                       | see notes               | see notes                                                                                                                                | see notes                                                             | wrap hop-specific criteria in a set of parentheses, use array position to indicate hop number. No hops indicates the opposite of hops().                                                             |
| Path Trace       | mpls                         | \[==]                   | null                                                                                                                                     | `((hops((mpls != null))))`                                            | use in conjunction with hops() or nohops()                                                                                                                                                           |
| Path Trace       | dscp                         | \[==, !=]               | Integer                                                                                                                                  | `((dscp != 26))`                                                      | set DSCP value received by target agent. use in conjunction with hops() or nohops()                                                                                                                  |
| Path Trace       | ip                           | \[in, !in]              | list                                                                                                                                     | `((hops[-1]((ip !in {"20.0.0.1", "10.0.0.0/8"}))))`                   | use in conjunction with hops() or nohops(). example shows last hop before destination.                                                                                                               |
| Path Trace       | asn                          | \[in, !in]              | list                                                                                                                                     | `((hops((asn !in {1111, 65536}))))`                                   | use in conjunction with hops() or nohops().                                                                                                                                                          |
| Path Trace       | rdns                         | \[in, !in]              | list                                                                                                                                     | `((hops((rdns !in {"*.facebook.com", "*.google.com"}))))`             | use in conjunction with hops() or nohops().                                                                                                                                                          |
| BGP              | reachability                 | \[<, <=, ==, !=, >=, >] | Integer + %                                                                                                                              | `((reachability <= 90%))`                                             | ensure you set percentage as part of the expression                                                                                                                                                  |
| BGP              | changes                      | \[<, <=, ==, !=, >=, >] | Float                                                                                                                                    | `((changes >= 1.1))`                                                  | ensure you set percentage as part of the expression                                                                                                                                                  |
| BGP              | prefixLengthIPv4             | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((prefixLengthIPv4 >= 23))`                                          | typically used in compound statements where covered prefixes are monitored                                                                                                                           |
| BGP              | prefixLengthIPv6             | \[<, <=, ==, !=, >=, >] | Integer                                                                                                                                  | `((prefixLengthIPv4 >= 47))`                                          | typically used in compound statements where covered prefixes are monitored                                                                                                                           |
| BGP              | prefix                       | \[in, !in]              | list                                                                                                                                     | `((prefix !in {"10.0.0.0/18"}))`                                      | typically used in compound statements where covered prefixes are monitored                                                                                                                           |
| BGP              | subprefix                    | \[in, !in]              | list                                                                                                                                     | `((subprefix !in {"10.1.0.0/24"}))`                                   | typically used in compound statements where covered prefixes are monitored                                                                                                                           |
| BGP              | bgpHops                      | see notes               | see notes                                                                                                                                | see notes                                                             | an array representing AS Path for BGP monitors. Use array index to identify hops from origin, use negative array index to identify hops from monitor, or no index to represent the entire array.     |
| BGP              | noBgpHops                    | see notes               | see notes                                                                                                                                | see notes                                                             | an array representing AS Path for BGP monitors. Use array index to identify hops from origin, use negative array index to identify hops from monitor, or no index to represent the entire array.     |
| BGP              | asn                          | \[in, !in]              | list                                                                                                                                     | `((bgpHops[1]((asn in {6}))))`                                        | use in conjunction with bgpHops() or noBgpHops()                                                                                                                                                     |

[`POST /v6/alert-rules/new` Creating an alert rule](broken-reference)

Creates a new alert rule in your account, based on properties provided in the POST data. In order to create a new alert rule, the user attempting the creation must be in a role that has the Edit alert rules permission. Users without this permission will receive an error.

Note: when assigning any alert rule to a test (which can be done as part of the creation activity), the user must be in a role that has the Edit tests permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* request body must contain fields to be set during creation. See the [Alert Rule Metadata](broken-reference) page for fields available during alert rule creation.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl https://api.thousandeyes.com/v6/alert-rules/new \ -H 'Content-Type: application/json' \ -u {email}:{authToken} \ -d '{ "alertType": "FTP", "default": 0, "expression": "((reachability < 90%))", "minimumSources": 10, "notes": "FTP Alert rule created using write api", "description": "TE FTP Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "FTP Alert Rule", "sourceMeasure": "percent", "testIds": [ 1001, 1002 ], "severity": "INFO" }'`

#### Response <a href="#response" id="response"></a>

If successful, will respond with an HTTP/201 response and a body which contains the new alert rule definition.

`HTTP/1.1 201 CREATED Server: nginx Date: Mon, 01 August 2019 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1492608660 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "alertRuleId": 2111, "alertType": "FTP", "default": 0, "expression": "((reachability < 90%))", "minimumSources": 10, "notes": "FTP Alert rule created using write api", "description": "TE FTP Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "FTP Alert Rule", "sourceMeasure": "percent", "testIds": [ 1001, 1002 ], "severity": "INFO" }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/alert-rules/{ruleId}/update` Updating an alert rule](broken-reference)

Modifies an existing alert rule in your account, based on properties provided in the POST data. In order to modify an alert rule, the user attempting the creation must be in a role that has the Edit alert rules permission. Users without this permission will receive an error.

Note: when assigning any alert rule to a test (which can be done as part of the update activity), the user must be in a role that has the Edit tests permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{ruleId}` corresponds to a ruleId returned by the `/alert-rules` endpoint.
* request body must contain a full list of fields. It is recommended to make a request to the `alert-rules/{ruleId}` endpoint and modify the conditions of the alert rule based on fields returned in that request. See the [Alert Rule Metadata](broken-reference) page for fields available during alert rule modification.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl https://api.thousandeyes.com/v6/alert-rules/123/update \ -H 'Content-Type: application/json' \ -u {email}:{authToken} \ -d '{ "alertType": "FTP", "default": 0, "expression": "((reachability < 90%))", "minimumSources": 10, "notes": "FTP Alert rule created using write api", "description": "TE FTP Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "FTP Alert Rule", "sourceMeasure": "percent", "testIds": [ 1001, 1002 ], "severity": "INFO" }'`

#### Response <a href="#response" id="response"></a>

If successful, will respond with an HTTP/200 response and the modified rule definition in the body.

`HTTP/1.1 200 OK Date: Fri, 12 Jul 2019 22:06:04 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive X-Server-Name: ldkvx Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1562969220 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "alertRuleId": 1234, "alertType": "FTP", "default": 0, "expression": "((reachability < 90%))", "minimumSources": 10, "notes": "FTP Alert rule created using write api", "description": "TE FTP Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "FTP Alert Rule", "sourceMeasure": "percent", "testIds": [ 1001, 1002 ], "severity": "INFO" }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/alert-rules/{ruleId}/delete` Deleting an alert rule](broken-reference)

Deletes an alert rule in your account. In order to delete an alert rule, the user attempting the creation must be in a role that has the Edit alert rules permission, as well as Edit Tests permission, in the event that the alert rule is assigned to any tests. Users without appropriate permissions will receive an error.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{ruleId}` corresponds to a ruleId returned by the `/alert-rules` endpoint.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/alert-rules/1234/delete.json \ -d '' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Response header will be returned as HTTP/204 response code. No response body will be returned.

`HTTP/1.1 204 No Content Date: Fri, 12 Jul 2019 22:11:49 GMT Connection: keep-alive X-Server-Name: 9gxxn Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1562969520 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/integrations` Alert notification integrations](broken-reference)

Returns a list of all alert notification integrations (webhooks, PagerDuty, Slack, …)

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/integrations.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns an object with two array properties: _thirdParty_ and _webhook_.

_thirdParty_ array objects reflect the following content:

| Field           | Data Type | Units | Notes                                            |
| --------------- | --------- | ----- | ------------------------------------------------ |
| integrationId   | string    | n/a   | unique ID of the integration                     |
| integrationName | string    | n/a   | name of the integration                          |
| integrationType | string    | n/a   | type of the integration, `PAGER_DUTY` or `SLACK` |
| target          | string    | n/a   | target URL of the integration                    |
| authMethod      | string    | n/a   | (PagerDuty only) always set to `Auth Token`      |
| authUser        | string    | n/a   | (PagerDuty only) PagerDuty user                  |
| authToken       | string    | n/a   | (PagerDuty only) authentication token            |
| channel         | string    | n/a   | (Slack only) Slack `#channel` or `@user`         |

_webhook_ array objects reflect the following content:

| Field           | Data Type | Units | Notes                                            |
| --------------- | --------- | ----- | ------------------------------------------------ |
| integrationId   | string    | n/a   | unique ID of the integration                     |
| integrationName | string    | n/a   | name of the integration                          |
| integrationType | string    | n/a   | type of the integration, always set to `WEBHOOK` |
| target          | string    | n/a   | target URL of the integration                    |

**Body**

`{ "integrations": { "thirdParty": [ { "authMethod": "Auth Token", "authToken": "0a4693462246893f9393ed8ab2bf22f69", "authUser": "te", "integrationId": "pa-52371", "integrationName": "Jira Thousandeyes", "integrationType": "PAGER_DUTY" }, { "channel": "@primoz", "integrationId": "sl-7976", "integrationName": "ThousandEyes Private", "integrationType": "SLACK", "target": "https://hooks.slack.com/services/T3G3DA1EY/B3243AG4Q/kwGHQz126speipc3E0e0Hx" } ], "webhook": [ { "integrationId": "wb-4563", "integrationName": "Alert ThousandEyes", "integrationType": "WEBHOOK", "target": "https://webhooker.example.com/alert/z126g4a3f2a" } ] } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/alert-suppression-windows` Alert suppression windows](broken-reference)

Returns a list of all alert suppression windows configured in your account group.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alert-suppression-windows.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns an alert suppression window object.

| Field                      | Data Type     | Units               | Notes                                                                                                                                                          |
| -------------------------- | ------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertSuppressionWindowId   | integer       | n/a                 | unique ID of the alert suppression window                                                                                                                      |
| alertSuppressionWindowName | string        | n/a                 | name of the alert suppression window                                                                                                                           |
| enabled                    | bit           | n/a                 | 0 for disabled, 1 for enabled                                                                                                                                  |
| status                     | string        | n/a                 | \[ACTIVE, INACTIVE, ENDED], indicates the current status of the suppression window                                                                             |
| startDateTime              | dateTime      | yyyy-MM-dd hh:mm:ss | the date/time when the alert suppression window will start.                                                                                                    |
| timezone                   | string        | n/a                 | timezone name, in Area/Location format, as specified in the IANA TZDB.                                                                                         |
| duration                   | integer       | seconds             | number of seconds for which the suppression window will be active                                                                                              |
| repeat                     | repeat object | n/a                 | see repeat options found below                                                                                                                                 |
| repeat.type                | string        | n/a                 | \[DAY, WEEK, MONTH, CUSTOM]                                                                                                                                    |
| repeat.intervalType        | string        | n/a                 | \[DAY, WEEK, MONTH]                                                                                                                                            |
| repeat.intervalLength      | integer       | n/a                 | number of intervalTypes to wait before reactivating the alert suppression window.                                                                              |
| repeat.daysOfWeek          | string        | n/a                 | Specify which day of the week the alert suppression window needs to be activated for. Only valid for intervalType = WEEK. \[SUN, MON, TUE, WED, THU, FRI, SAT] |
| endRepeat                  | repeat object | n/a                 | see endRepeat options found below                                                                                                                              |
| endRepeat.type             | string        | n/a                 | \[COUNT, NEVER, DATE]                                                                                                                                          |
| endRepeat.count            | integer       | n/a                 | end repeat after number of occurrences (only valid with COUNT type option)                                                                                     |
| endRepeat.date             | date          | yyyy-MM-dd          | end repeat after specific date (only valid with DATE type option)                                                                                              |

**Body**

`{ "alertSuppressionWindows": [ { "alertSuppressionWindowId": 2411, "alertSuppressionWindowName": "Monthly maintenance", "duration": 300, "enabled": 0, "endRepeat": { "type": "NEVER" }, "repeat": { "type": "MONTH" }, "startDateTime": "2017-07-01 05:00:00", "status": "INACTIVE", "timezone": "UTC" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/alert-suppression-windows/{alertSuppressionWindowId}` Alert suppression window detail](broken-reference)

Returns details for an alert suppression window configured in your account group.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* {alertSuppressionWindowId} corresponds to the id of an alertSuppressionWindow, see the alert suppression window list endpoint for a listing of alert suppression windows.
* No request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alert-suppression-windows/2411.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns an alert suppression window object’s details, along with configured tests.

| Field                      | Data Type                           | Units               | Notes                                                                                                                                                          |
| -------------------------- | ----------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertSuppressionWindowId   | integer                             | n/a                 | unique ID of the alert suppression window                                                                                                                      |
| alertSuppressionWindowName | string                              | n/a                 | name of the alert suppression window                                                                                                                           |
| enabled                    | bit                                 | n/a                 | 0 for disabled, 1 for enabled                                                                                                                                  |
| status                     | string                              | n/a                 | \[ACTIVE, INACTIVE, ENDED], indicates the current status of the suppression window                                                                             |
| tests                      | array of {“testId”: testId} objects | n/a                 | List of tests assigned to the alert suppression window: \[{“testId”: 123}, {“testId”: 456}]                                                                    |
| startDateTime              | dateTime                            | yyyy-MM-dd hh:mm:ss | the date/time when the alert suppression window will start.                                                                                                    |
| timezone                   | string                              | n/a                 | timezone name, in Area/Location format, as specified in the IANA TZDB.                                                                                         |
| duration                   | integer                             | seconds             | number of seconds for which the suppression window will be active                                                                                              |
| repeat                     | repeat object                       | n/a                 | see repeat options found below                                                                                                                                 |
| repeat.type                | string                              | n/a                 | \[DAY, WEEK, MONTH, CUSTOM]                                                                                                                                    |
| repeat.intervalType        | string                              | n/a                 | \[DAY, WEEK, MONTH]                                                                                                                                            |
| repeat.intervalLength      | integer                             | n/a                 | number of intervalTypes to wait before reactivating the alert suppression window.                                                                              |
| repeat.daysOfWeek          | string                              | n/a                 | Specify which day of the week the alert suppression window needs to be activated for. Only valid for intervalType = WEEK. \[SUN, MON, TUE, WED, THU, FRI, SAT] |
| endRepeat                  | repeat object                       | n/a                 | see endRepeat options found below                                                                                                                              |
| endRepeat.type             | string                              | n/a                 | \[COUNT, NEVER, DATE]                                                                                                                                          |
| endRepeat.count            | integer                             | n/a                 | end repeat after number of occurrences (only valid with COUNT type option)                                                                                     |
| endRepeat.date             | date                                | yyyy-MM-dd          | end repeat after specific date (only valid with DATE type option)                                                                                              |

**Body**

`{ "alertSuppressionWindows": [ { "alertSuppressionWindowId": 2411, "alertSuppressionWindowName": "Monthly maintenance", "duration": 300, "enabled": 0, "endRepeat": { "type": "NEVER" }, "repeat": { "type": "MONTH" }, "startDateTime": "2017-07-01 05:00:00", "status": "INACTIVE", "tests": [ { "alertsEnabled": 1, "apiLinks": [...], "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 20:44:05", "domain": "thousandeyes.com ANY", "enabled": 1, "interval": 900, "liveShare": 0, "modifiedBy": "API Sandbox Admin (api.sandbox+admin@thousandeyes.com)", "modifiedDate": "2017-06-19 18:53:39", "savedEvent": 0, "testId": 820, "testName": "thousandeyes.com ANY", "type": "dns-trace" }, ... ], "timezone": "UTC" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/alert-suppression-windows/new` Creating an alert suppression window](broken-reference)

Creates a new alert suppression window in ThousandEyes, based on properties provided in the POST data. In order to create a new alert suppression window, the user attempting the creation must be an Account Admin.

Regular users are blocked from using any of the POST-based methods.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* request body containing the following fields:

| Field                      | Data Type                           | Units               | Notes                                                                                                                                                          |
| -------------------------- | ----------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertSuppressionWindowName | string                              | n/a                 | name of the alert suppression window                                                                                                                           |
| enabled                    | bit                                 | n/a                 | 0 for disabled, 1 for enabled                                                                                                                                  |
| tests                      | array of {“testId”: testId} objects | n/a                 | List of tests assigned to the alert suppression window: \[{“testId”: 123}, {“testId”: 456}]                                                                    |
| startDateTime              | dateTime                            | yyyy-MM-dd hh:mm:ss | the date/time when the alert suppression window will start.                                                                                                    |
| timezone                   | string                              | n/a                 | timezone name, in Area/Location format, as specified in the IANA TZDB.                                                                                         |
| duration                   | integer                             | seconds             | number of seconds for which the suppression window will be active                                                                                              |
| repeat                     | repeat object                       | n/a                 | see repeat options found below                                                                                                                                 |
| repeat.type                | string                              | n/a                 | \[DAY, WEEK, MONTH, CUSTOM]                                                                                                                                    |
| repeat.intervalType        | string                              | n/a                 | \[DAY, WEEK, MONTH]                                                                                                                                            |
| repeat.intervalLength      | integer                             | n/a                 | number of intervalTypes to wait before reactivating the alert suppression window.                                                                              |
| repeat.daysOfWeek          | string                              | n/a                 | Specify which day of the week the alert suppression window needs to be activated for. Only valid for intervalType = WEEK. \[SUN, MON, TUE, WED, THU, FRI, SAT] |
| endRepeat                  | repeat object                       | n/a                 | see endRepeat options found below                                                                                                                              |
| endRepeat.type             | string                              | n/a                 | \[COUNT, NEVER, DATE]                                                                                                                                          |
| endRepeat.count            | integer                             | n/a                 | end repeat after number of occurrences (only valid with COUNT type option)                                                                                     |
| endRepeat.date             | date                                | yyyy-MM-dd          | end repeat after specific date (only valid with DATE type option)                                                                                              |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alert-suppression-windows/new.json \ -d '{ "alertSuppressionWindowName": "30 min asw created asw via API", "enabled": 1, "startDateTime": "2017-03-15 00:00:00", "timezone": "America/Los_Angeles", "duration": 1800, "repeat": { "type": "DAY" }, "endRepeat": { "type": "NEVER" } }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If an alert suppression window is successfully created, an HTTP/201 CREATED response will be returned, and the alert suppression window detail will be returned. See the example below:

**Body**

`{ "alertSuppressionWindows": [ { "alertSuppressionWindowId": 230, "alertSuppressionWindowName": "30 min asw created asw via API", "enabled": 1, "status": "INACTIVE", "tests": [], "startDateTime": "2017-03-15 07:00:00", "timezone": "America/Los_Angeles", "duration": 1800, "repeat": { "type": "DAY" }, "endRepeat": { "type": "NEVER" } } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/alert-suppression-windows/{alertSuppressionWindowId}/update` Updating an alert suppression window](broken-reference)

Updates an alert suppression window in ThousandEyes, based on properties provided in the POST data. In order to modify an alert suppression window, the user attempting the update must be an Account Admin.

Regular users are blocked from using any of the POST-based methods.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* {alertSuppressionWindowId} corresponds to the id of an alertSuppressionWindow, see the alert suppression window list endpoint for a listing of alert suppression windows.
* Request body containing the following fields

| Field                      | Data Type                           | Units               | Notes                                                                                                                                                          |
| -------------------------- | ----------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertSuppressionWindowName | string                              | n/a                 | name of the alert suppression window                                                                                                                           |
| enabled                    | bit                                 | n/a                 | 0 for disabled, 1 for enabled                                                                                                                                  |
| tests                      | array of {“testId”: testId} objects | n/a                 | List of tests assigned to the alert suppression window: \[{“testId”: 123}, {“testId”: 456}]                                                                    |
| startDateTime              | dateTime                            | yyyy-MM-dd hh:mm:ss | the date/time when the alert suppression window will start.                                                                                                    |
| timezone                   | string                              | n/a                 | timezone name, in Area/Location format, as specified in the IANA TZDB.                                                                                         |
| duration                   | integer                             | seconds             | number of seconds for which the suppression window will be active                                                                                              |
| repeat                     | repeat object                       | n/a                 | see repeat options found below                                                                                                                                 |
| repeat.type                | string                              | n/a                 | \[DAY, WEEK, MONTH, CUSTOM]                                                                                                                                    |
| repeat.intervalType        | string                              | n/a                 | \[DAY, WEEK, MONTH]                                                                                                                                            |
| repeat.intervalLength      | integer                             | n/a                 | number of intervalTypes to wait before reactivating the alert suppression window.                                                                              |
| repeat.daysOfWeek          | string                              | n/a                 | Specify which day of the week the alert suppression window needs to be activated for. Only valid for intervalType = WEEK. \[SUN, MON, TUE, WED, THU, FRI, SAT] |
| endRepeat                  | repeat object                       | n/a                 | see endRepeat options found below                                                                                                                              |
| endRepeat.type             | string                              | n/a                 | \[COUNT, NEVER, DATE]                                                                                                                                          |
| endRepeat.count            | integer                             | n/a                 | end repeat after number of occurrences (only valid with COUNT type option)                                                                                     |
| endRepeat.date             | date                                | yyyy-MM-dd          | end repeat after specific date (only valid with DATE type option)                                                                                              |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/alert-suppression-windows/230/update.json \ -d '{ "alertSuppressionWindowName": "30 min asw created asw via API -- modified to be 60 mins", "enabled": 1, "startDateTime": "2017-03-15 00:00:00", "timezone": "America/Los_Angeles", "duration": 3600, "repeat": { "type": "DAY" }, "endRepeat": { "type": "NEVER" } }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If an alert suppression window is successfully created, an HTTP/200 OK response will be returned, and the alert suppression window detail will be returned. See the example below:

**Body**

`{ "alertSuppressionWindows": [ { "alertSuppressionWindowId": 230, "alertSuppressionWindowName": "30 min asw created asw via API -- modified to be 60 mins", "enabled": 1, "status": "INACTIVE", "tests": [], "startDateTime": "2017-03-15 07:00:00", "timezone": "America/Los_Angeles", "duration": 3600, "repeat": { "type": "DAY" }, "endRepeat": { "type": "NEVER" } } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/alert-suppression-windows/{alertSuppressionWindowId}/delete` Deleting an alert suppression window](broken-reference)

Deletes an alert suppression window.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* {alertSuppressionWindowId} corresponds to the id of an alertSuppressionWindow, see the alert suppression window list endpoint for a listing of alert suppression windows.
* No request body

#### Example <a href="#example" id="example"></a>

`$ curl -i https://api.thousandeyes.com/v6/alert-suppression-windows/217/delete.json \ -d '' \ -u {email}:{authToken} -H "Content-Type: application/json"`

#### Response <a href="#response" id="response"></a>

If an alert suppression window is successfully deleted, an HTTP/204 NO CONTENT response will be returned, and an empty JSON response will be in the body of the response.

`HTTP/1.1 204 NO CONTENT Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493373360 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-1`

**Body**

* The body of a delete request will be empty.

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[Creating an advanced Alert Rule](broken-reference)

* When creating an alert rule from API the alerting logic is specified in the `expression` Keyword. Below are examples for complex Alert Rules which apply to a specific set of Agents and have other complex logic.

### Alert only for specific agents <a href="#alert_only_for_specific_agents" id="alert_only_for_specific_agents"></a>

* Alert rules applicable to specific agents can be created by adding a `locationId` keyword with an `in` operator, followed by agentIds of the Agents applicable to the rule.

#### Example Expression <a href="#example_expression" id="example_expression"></a>

`$ curl https://api.thousandeyes.com/v6/alert-rules/new \ -H 'Content-Type: application/json' \ -u {email}:{authToken} \ -d '{ "alertType": "HTTP Server", "default": 0, "expression": "[(locationId in {\"58\", \"25\", \"7815\"})]((probDetail != \"\"))", "minimumSources": 10, "notes": "HTTP Alert rule for agentIds 58, 25 and 7815 only", "description": "TE HTTP Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "HTTP Server Alert Rule", "sourceMeasure": "percent", "testIds": [ 1001, 1002 ], "severity": "INFO" }'`

#### Response <a href="#response" id="response"></a>

If successful, will respond with an HTTP/201 response and a body which contains the new alert rule definition.

### Alert except specific agents <a href="#alert_except_specific_agents" id="alert_except_specific_agents"></a>

* Alert rule applicable to **all agents except** specific agents can be created by appending a `locationId` with a `!in` operator followed by `agentId`s of desired agents to the expression.

#### Example Expression <a href="#example_expression" id="example_expression"></a>

`$ curl https://api.thousandeyes.com/v6/alert-rules/new \ -H 'Content-Type: application/json' \ -u {email}:{authToken} \ -d '{ "alertType": "HTTP Server", "default": 0, "expression": "[(locationId !in {\"58\", \"25\", \"7815\"})]((probDetail != \"\"))", "minimumSources": 10, "notes": "HTTP Alert rule for all agentIds except 58, 25 and 7815", "description": "TE HTTP Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "HTTP Server Alert Rule", "sourceMeasure": "percent", "testIds": [ 1001, 1002 ], "severity": "INFO" }'`

#### Response <a href="#response" id="response"></a>

If successful, will respond with an HTTP/201 response and a body which contains the new alert rule definition.

### Alert when ALL conditions match <a href="#alert_when_all_conditions_match" id="alert_when_all_conditions_match"></a>

* Multiple conditions can be compounded with the `&&` (AND) operator in an `expression` to alert when **All** conditions match.

#### Example Expression <a href="#example_expression" id="example_expression"></a>

`$ curl https://api.thousandeyes.com/v6/alert-rules/new \ -H 'Content-Type: application/json' \ -u {email}:{authToken} \ -d '{ "alertType": "End-to-End (Agent)", "default": 0, "expression": "((probDetail != \"\") && (loss <= 10%) && (latency <= 50 ms))", "minimumSources": 10, "notes": "Alert only when all conditions match", "description": "TE Agent to Agent Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "direction": "TO_TARGET", "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "Agent to Agent Alert Rule", "sourceMeasure": "percent", "testIds": [ 1003, 1004 ], "severity": "INFO" }'`

#### Response <a href="#response" id="response"></a>

If successful, will respond with an HTTP/201 response and a body which contains the new alert rule definition.

### Alert when ANY conditions match <a href="#alert_when_any_conditions_match" id="alert_when_any_conditions_match"></a>

* Multiple conditions can be combined with the `||` (OR) operator in an `expression` to alert when **ANY** conditions match.

#### Example Expression <a href="#example_expression" id="example_expression"></a>

`$ curl https://api.thousandeyes.com/v6/alert-rules/new \ -H 'Content-Type: application/json' \ -u {email}:{authToken} \ -d '{ "alertType": "End-to-End (Agent)", "default": 0, "expression": "((probDetail != \"\") || (loss <= 10%) || (latency <= 50 ms))", "minimumSources": 10, "notes": "Alert when any conditions match", "description": "TE Agent to Agent Alert rule with write api", "notifications": { "email": { "message": "", "recipient": [ "noreply@thousandeyes.com" ] }, "thirdParty": [ { "integrationId": "sl-101", "integrationType": "SLACK" } ], "webhook": [ { "integrationId": "wb-201", "integrationType": "WEBHOOK" } ] }, "notifyOnClear": 1, "direction": "BIDIRECTIONAL", "roundsViolatingOutOf": 10, "roundsViolatingRequired": 10, "roundsViolatingMode": "ANY", "ruleName": "Agent to Agent Alert Rule", "sourceMeasure": "percent", "testIds": [ 1005, 1006 ], "severity": "INFO" }'`

#### Response <a href="#response" id="response"></a>

If successful, will respond with an HTTP/201 response and a body which contains the new alert rule definition.

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
