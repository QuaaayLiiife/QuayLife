# Endpoint Scheduled Tests

### Endpoint Scheduled Tests

[`GET /v6/endpoint-tests` Scheduled Test List](broken-reference)

Returns a list of all endpoint scheduled tests configured in ThousandEyes. This list does not contain saved events.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Sends back an array of endpoint tests. See [Scheduled Endpoint Test Metadata](broken-reference) page for information on fields returned by this endpoint.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-tests.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointTest": [ { "alertsEnabled": 0, "apiLinks": [...], "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2018-08-25 16:56:50", "enabled": 1, "interval": 60, "agentSelectorConfig": { "agentIds": [], "agentSelectorType": "LIST_OF_LABELS", "labelIds": [10581, 12461], "maxMachines": 25 }, "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedDate": "2018-08-25 16:57:59", "mtuMeasurements": 0, "networkMeasurements": 1, "port": -1, "protocol": "ICMP", "savedEvent": 0, "server": "www.thousandeyes.com", "testId": 282, "testName": "ThousandeEyes", "type": "agent-to-server", "usePublicBgp": 0 }, ... ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-tests/{testType}` Scheduled Test List by Type](broken-reference)

Returns a list of all endpoint scheduled tests of the type specified, configured in ThousandEyes. The list does not contain saved events.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testType}` corresponds to any of the following options:
  * agent-to-server
  * http-server
* There is no request body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-tests/http-server.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of tests matching the requested test type. See [Scheduled Endpoint Test Metadata](broken-reference) page for information on fields returned by this endpoint.

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:54 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 238 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-1`

**Body**

`{ "endpointTest": [ { "alertsEnabled": 0, "apiLinks": [...], "authType": "NONE", "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "API Sandbox User (noprely@thousandeyes.com)", "createdDate": "2018-08-18 18:33:23", "enabled": 1, "followRedirects": 1, "httpTargetTime": 1000, "httpTimeLimit": 5000, "httpVersion": 1, "interval": 60, "agentSelectorConfig": { "agentIds": ["LAPTOP-MAC-AGENT", "PC-WINDOWS-AGENT"], "agentSelectorType": "SPECIFIC_AGENTS", "labelIds": [], "maxMachines": 25 }, "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedDate": "2018-08-25 17:22:54", "mtuMeasurements": 0, "networkMeasurements": 1, "port": 443, "protocol": "TCP", "savedEvent": 0, "server": "developer.thousandeyes.com", "sslVersion": "Auto", "sslVersionId": 0, "testId": 273, "testName": "Developer Reference", "type": "http-server", "url": "https://developer.thousandeyes.com/", "useNtlm": 0, "usePublicBgp": 0, "username": "", "verifyCertificate": 1 }, ... ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-tests/{testId}` Scheduled Test Details](broken-reference)

Returns details for an endpoint scheduled test, including test type, name, intervals, targets and alert rules.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the endpoint scheduled test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Sends back all metadata for the requested endpoint scheduled test. See [Scheduled Endpoint Test Metadata](broken-reference) page for more information on fields returned by this endpoint.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-tests/282.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:57 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 235 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-5`

**Body**

`{ "endpointTest": [ { "alertsEnabled": 0, "apiLinks": [...], "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2018-08-25 16:56:50", "enabled": 1, "interval": 60, "agentSelectorConfig": { "agentIds": [], "agentSelectorType": "ANY_AGENT", "labelIds": [], "maxMachines": 25 }, "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedDate": "2018-08-25 16:57:59", "mtuMeasurements": 0, "networkMeasurements": 1, "port": -1, "protocol": "ICMP", "savedEvent": 0, "server": "www.thousandeyes.com", "testId": 282, "testName": "ThousandeEyes", "type": "agent-to-server", "usePublicBgp": 0 } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[Scheduled Test Metadata](broken-reference)

Endpoint test fields are shown in the table below.

Fields are listed alphabetically by test type below.

These fields are system-generated and read only, and displayed as part of test metadata.

| Test Type   | Field                                 | Data Type                 | Acceptable Values                                                                                                                         | Notes                                                                                         |
| ----------- | ------------------------------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| (all)       | alertsEnabled                         | integer                   | 0 or 1                                                                                                                                    | 1 to enable alerts, or 0 to disable alerts                                                    |
| (all)       | apiLinks                              | array of apiLinks objects | Array of apiLink objects, showing rel and href elements                                                                                   | Self links to endpoint to pull test metadata, and data links to endpoint for test data        |
| (all)       | bandwidthMeasurements                 | integer                   | 0 or 1                                                                                                                                    | 1 to measure bandwidth                                                                        |
| (all)       | bgpMeasurements                       | integer                   | 0 or 1                                                                                                                                    | 1 to enable bgp measurements                                                                  |
| (all)       | createdBy                             | string                    | Username (email@company.com)                                                                                                              | User’s email                                                                                  |
| (all)       | createdDate                           | string                    | YYYY-MM-DD HH:mm:ss formatted date                                                                                                        | Shown in UTC                                                                                  |
| (all)       | enabled                               | integer                   | 0 or 1                                                                                                                                    | 1 to enable the test, 0 to disable the test                                                   |
| (all)       | interval                              | integer                   | \[60, 120, 300, 600, 900, 1800, 3600]                                                                                                     | Value in seconds                                                                              |
| (all)       | agentSelectorConfig                   | object                    | {agentIds: array of strings, agentSelectorType: enum value, labelIds: array of longs, maxMachines: \[1-10000]}                            | Agent selection object                                                                        |
| (all)       | agentSelectorConfig.agentIds          | array of strings          | see notes                                                                                                                                 | List of agent ids. Must be set if agentSelectorType == SPECIFIC\_AGENTS                       |
| (all)       | agentSelectorConfig.agentSelectorType | string                    | ANY\_AGENT, SPECIFIC\_AGENTS, LIST\_OF\_LABELS                                                                                            | Agent selection type: either all agents available, or list of agents, of list of agent labels |
| (all)       | agentSelectorConfig.labelIds          | array of longs            | see notes                                                                                                                                 | List of label ids. Must be set if agentSelectorType == LIST\_OF\_LABELS                       |
| (all)       | agentSelectorConfig.maxMachines       | integer                   | \[1-10000]                                                                                                                                | Upper limit of machines for the test                                                          |
| (all)       | modifiedBy                            | string                    | Username (email@company.com)                                                                                                              | User’s email                                                                                  |
| (all)       | modifiedDate                          | string                    | YYYY-MM-DD HH:mm:ss formatted date                                                                                                        | Shown in UTC                                                                                  |
| (all)       | mtuMeasurements                       | integer                   | 0 or 1                                                                                                                                    | 1 to measure MTU sizes on network tests                                                       |
| (all)       | networkMeasurements                   | integer                   | 0 or 1                                                                                                                                    | 1 to perform network tests                                                                    |
| (all)       | port                                  | integer                   | (1..65535)                                                                                                                                | TCP port used to perform the test; if ICMP is selected, -1 is returned                        |
| (all)       | protocol                              | string                    | `TCP` or `ICMP`                                                                                                                           | Protocol used to perform the test                                                             |
| (all)       | savedEvent                            | integer                   | 0 or 1                                                                                                                                    | Indicates 1 for a saved event, 0 for a normal test                                            |
| (all)       | server                                | string                    | (any)                                                                                                                                     | Target domain name or IP address                                                              |
| (all)       | testId                                | integer                   | unique ID of test                                                                                                                         | Each test is assigned a unique ID; this is used to access test data from other endpoints      |
| (all)       | testName                              | string                    | (any)                                                                                                                                     | Test name must be unique                                                                      |
| (all)       | type                                  | string                    | type of test being queried                                                                                                                | Test type is implicit in the test creation url                                                |
| (all)       | usePublicBgp                          | integer                   | 0 or 1                                                                                                                                    | Use all the public BGP montiors                                                               |
| HTTP Server | authType                              | string                    | “NONE”, “BASIC”, or “NTLM”                                                                                                                | Type of authentication for the test                                                           |
| HTTP Server | contentRegex                          | string                    | [Regular Expressions](https://docs.thousandeyes.com/product-documentation/tests/posix-extended-regular-expression-syntax-quick-reference) | This field does not require escaping                                                          |
| HTTP Server | followRedirects                       | integer                   | 0 or 1                                                                                                                                    | 0 to not follow HTTP/301 or HTTP/302 redirect directives.                                     |
| HTTP Server | httpTargetTime                        | integer                   | (100..5000)                                                                                                                               | Target time for HTTP server completion; specified in milliseconds                             |
| HTTP Server | httpTimeLimit                         | integer                   | (5000..60000)                                                                                                                             | Target time for HTTP Server timeout; specified in milliseconds                                |
| HTTP Server | httpVersion                           | integer                   | \[1,2]                                                                                                                                    | 2 for prefer HTTP/2, 1 for HTTP/1.1 only                                                      |
| HTTP Server | postBody                              | string                    | see notes                                                                                                                                 | If the post body is set to something other than empty, the requestMethod will be set to POST  |
| HTTP Server | sslVersion                            | string                    | corresponds to sslVersionId                                                                                                               | Reflects the verbose ssl protocol version used by a test                                      |
| HTTP Server | sslVersionId                          | integer                   | \[0,3,4,5,6]                                                                                                                              | 0 for default (Auto), 6 for TLS1.2, 5 for TLS1.1, 4 for TLS1.0, 3 for SSLv3                   |
| HTTP Server | url                                   | string                    | see notes                                                                                                                                 | Target for the test                                                                           |
| HTTP Server | useNtlm                               | integer                   | 0 or 1                                                                                                                                    | 1 for NTLM, 0 for Basic Authentication. Requires username/password to be set                  |
| HTTP Server | userAgent                             | string                    | see notes                                                                                                                                 | user-agent string to be provided during the test                                              |
| HTTP Server | username                              | string                    | see notes                                                                                                                                 | username to be used for Basic/NTLM authentication                                             |
| HTTP Server | verifyCertificate                     | integer                   | 0 or 1                                                                                                                                    | 0 to ignore certificate errors                                                                |

[`POST /v6/endpoint-tests/{testType}/new` Creating a Scheduled Test](broken-reference)

Creates a new Endpoint test in ThousandEyes, based on properties provided in the POST data. In order to create a new test, the user attempting the creation must be an Account Admin.

Regular users are blocked from using any of the POST-based methods.

#### Request <a href="#request" id="request"></a>

* `{testType}` corresponds to any of the following options:
  * `agent-to-server` - endpoint network test
  * `http-server` - endpoint http test
* Request body should contain fields to be set during creation.

**Example - http test**

`$ curl -i https://api.thousandeyes.com/v6/endpoint-tests/http-server/new.json \ -d '{ "authType": "NONE", "flagPing": true, "flagTraceroute": true, "agentSelectorType": "ANY_AGENT", "httpTimeLimit": 5000, "maxMachines": 5, "interval" : 3600, "sslVersion": 0, "targetResponseTime": 5000, "testName": "HTTP test", "url": "www.example.com", "verifyCertHostname": true }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

| Field              | Data Type        | Units                                          | Notes                                                                                                                                                                                                                   |
| ------------------ | ---------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentIds           | array of strings | n/a                                            | List of agent ids. Must be set if agentSelectorType == SPECIFIC\_AGENTS                                                                                                                                                 |
| agentSelectorType  | string           | ANY\_AGENT, SPECIFIC\_AGENTS, LIST\_OF\_LABELS | Agent selection type: either all agents available, or list of agents, of list of agent labels                                                                                                                           |
| authType           | string           | n/a                                            | Authentication type: NONE, BASIC or NTLM                                                                                                                                                                                |
| flagPing           | boolean          | n/a                                            | Optional flag indicating if test should run ping. If not specified, true is used by default                                                                                                                             |
| flagTraceroute     | boolean          | n/a                                            | Optional flag indicating if test should run traceroute. If not specified, true is used by default                                                                                                                       |
| groupId            | integer          | n/a                                            | (Deprecated) Unique ID of the label, which can be retrieved or created by [Labels API](https://developer.thousandeyes.com/v6/labels/). Should be substituted by combination of agentSelectorType, agentIds and labelIds |
| httpTimeLimit      | integer          | milliseconds                                   | Maximum amount of time in milliseconds the agents wait before a request times out                                                                                                                                       |
| interval           | integer          | \[120, 300, 600, 900, 1800, 3600]              | Interval in seconds that the test will execute on                                                                                                                                                                       |
| labelIds           | array of longs   | n/a                                            | List of label ids. Must be set if agentSelectorType == LIST\_OF\_LABELS                                                                                                                                                 |
| maxMachines        | integer          | \[1-100000]                                    | Upper limit of machines which can execute this test                                                                                                                                                                     |
| networkProtocol    | String           | n/a                                            | ICMP or TCP, default ICMP                                                                                                                                                                                               |
| password           | string           | n/a                                            | Password if authentication was specified to BASIC or NTLM                                                                                                                                                               |
| pathtraceInSession | String           | n/a                                            | First initiates a TCP session with the target server and sends path trace packets within that TCP session. Applicable only if TCP is selected as a network protocol                                                     |
| port               | integer          | n/a                                            | Port number, if not specified, the port is selected based on a protocol (HTTP 80, HTTPS 443)                                                                                                                            |
| sslVersion         | integer          | n/a                                            | Ssl protocol version (0 - AUTO, 3 - SSL v3, 4 - TLS v1.0, 5 - TLS 1.1, 6 - TLS 1.2)                                                                                                                                     |
| targetResponseTime | integer          | milliseconds                                   | Affects the colours of agents and legends on the view page. The value is compared with actual response time in order to determine the color scale (from green to red)                                                   |
| testName           | string           | n/a                                            | Name of the test                                                                                                                                                                                                        |
| tcpProbeMode       | String           | n/a                                            | TCP mode: AUTO, SYN or SACK. Applicable only if TCP is selected as a network protocol,                                                                                                                                  |
| url                | string           | n/a                                            | Test target URL, for example “www.example.com”. Optionally, it can specify a protocol (http or https). If the protocol is not specified, “https” is used by default                                                     |
| username           | string           | n/a                                            | User name if authentication was specified to BASIC or NTLM                                                                                                                                                              |
| verifyCertHostname | boolean          | n/a                                            | Flag indicating if a certificate should be verified                                                                                                                                                                     |

**Example - network test**

`$ curl -i https://api.thousandeyes.com/v6/endpoint-tests/agent-to-server/new.json \ -d '{ "flagPing": true, "flagTraceroute": true, "interval" : 3600, "agentSelectorType": "ANY_AGENT", "agentIds": ["LAPTOP-MAC-AGENT", "PC-WINDOWS-AGENT"], "maxMachines": 5, "serverName": "www.example.com", "port": 80, "testName": "Network test" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

| Field             | Data Type        | Units                                          | Notes                                                                                                                                                                                                                   |
| ----------------- | ---------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentIds          | array of strings | n/a                                            | List of agent ids. Must be set if agentSelectorType == SPECIFIC\_AGENTS                                                                                                                                                 |
| flagPing          | boolean          | n/a                                            | Optional flag indicating if test should run ping. If not specified, true is used by default                                                                                                                             |
| flagTraceroute    | boolean          | n/a                                            | Optional flag indicating if test should run traceroute. If not specified, true is used by default                                                                                                                       |
| groupId           | integer          | n/a                                            | (Deprecated) Unique ID of the label, which can be retrieved or created by [Labels API](https://developer.thousandeyes.com/v6/labels/). Should be substituted by combination of agentSelectorType, agentIds and labelIds |
| interval          | integer          | \[120, 300, 600, 900, 1800, 3600]              | Interval in seconds that the test will execute on                                                                                                                                                                       |
| labelIds          | array of longs   | n/a                                            | List of label ids. Must be set if agentSelectorType == LIST\_OF\_LABELS                                                                                                                                                 |
| maxMachines       | integer          | \[1-100000]                                    | Maximum number of agents which can execute this test                                                                                                                                                                    |
| agentSelectorType | string           | ANY\_AGENT, SPECIFIC\_AGENTS, LIST\_OF\_LABELS | Agent selection type: either all agents available, or list of agents, of list of agent labels                                                                                                                           |
| port              | integer          | n/a                                            | Port number, if not specified, it’s set to 80 by default                                                                                                                                                                |
| serverName        | string           | n/a                                            | A server address without a protocol (for example “www.example.com”) or IP address                                                                                                                                       |
| testName          | string           | n/a                                            | Name of the test                                                                                                                                                                                                        |

#### Response <a href="#response" id="response"></a>

If a test is successfully created, an HTTP/201 CREATED response will be returned, and the test definition will be returned. See the example below.

Response does not include the results of the test. Once the test has been run, results can be retrieved using [Endpoint Test Data](https://developer.thousandeyes.com/v6/endpoint\_test\_data) endpoints. API test data endpoints URLs are provided in test definition output upon test creation. See the example below.

`HTTP/1.1 201 Created Server: nginx Date: Mon, 17 Feb 2020 13:41:02 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1490622120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

**Body**

`{ "endpointTest": [ { "alertsEnabled": 0, "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/endpoint-data/tests/net/metrics/9902783", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/endpoint-data/tests/net/path-vis/9902783", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/endpoint-data/tests/web/http-server/9902783", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/endpoint-tests/9902783", "rel": "self" } ], "authType": "NONE", "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "API User (noprely@thousandeyes.com)", "createdDate": "2020-02-17 11:11:19", "enabled": 1, "followRedirects": 1, "httpTargetTime": 5000, "httpTimeLimit": 5000, "httpVersion": 1, "interval": 60, "agentSelectorConfig": { "agentIds": [], "agentSelectorType": "LIST_OF_LABELS", "labelIds": [10581, 12461], "maxMachines": 25 }, "modifiedBy": "API User (noprely@thousandeyes.com)", "modifiedDate": "2020-02-17 11:11:19", "mtuMeasurements": 0, "networkMeasurements": 1, "port": 443, "protocol": "TCP", "savedEvent": 0, "server": "www.example.com", "sslVersion": "Auto", "sslVersionId": 0, "testId": 9902783, "testName": "HTTP test", "type": "http-server", "url": "https://www.example.com", "useNtlm": 0, "usePublicBgp": 0, "username": "", "verifyCertificate": 1 } ] }`

[`GET /v6/endpoint-automated-session-tests` Automated Session Test List](broken-reference)

Returns a list of all endpoint automated session tests configured in ThousandEyes. This list does not contain saved events.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Sends back an array of endpoint automated session tests. See [Endpoint Automated Session Test Metadata](broken-reference) page for information on fields returned by this endpoint.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-automated-session-tests.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "automatedSessionTests": [ { "alertsEnabled": 0, "apiLinks": [...], "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2018-08-25 16:56:50", "enabled": 1, "interval": 60, "application": "WEBEX", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedDate": "2018-08-25 16:57:59", "mtuMeasurements": 0, "networkMeasurements": 1, "port": -1, "protocol": "ICMP", "savedEvent": 0, "server": "www.thousandeyes.com", "testId": 282, "testName": "ThousandeEyes", "type": "agent-to-server", "usePublicBgp": 0 }, ... ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-automated-session-tests/{testId}` Automated Session Test Details](broken-reference)

Returns details for an endpoint automated session test, including test type, name, intervals, targets.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the endpoint scheduled test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Sends back all metadata for the requested endpoint automated session test. See [Endpoint Automated Session Test Metadata](broken-reference) page for more information on fields returned by this endpoint.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-automated-session-tests/282.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:57 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 235 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-5`

**Body**

`{ "automatedSessionTests": [ { "alertsEnabled": 0, "apiLinks": [...], "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2018-08-25 16:56:50", "enabled": 1, "interval": 60, "application": "WEBEX", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedDate": "2018-08-25 16:57:59", "mtuMeasurements": 0, "networkMeasurements": 1, "port": -1, "protocol": "ICMP", "savedEvent": 0, "server": "www.thousandeyes.com", "testId": 282, "testName": "ThousandeEyes", "type": "agent-to-server", "usePublicBgp": 0 } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[Automated Session Test Metadata](broken-reference)

Endpoint Automated Session Test fields are shown in the table below.

Fields are listed alphabetically by test type below.

These fields are system-generated and read only, and displayed as part of test metadata.

| Field                 | Data Type                 | Acceptable Values                                       | Notes                                                                                    |
| --------------------- | ------------------------- | ------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| alertsEnabled         | integer                   | 0 or 1                                                  | 1 to enable alerts, or 0 to disable alerts                                               |
| apiLinks              | array of apiLinks objects | Array of apiLink objects, showing rel and href elements | Self links to endpoint to pull test metadata, and data links to endpoint for test data   |
| bandwidthMeasurements | integer                   | 0 or 1                                                  | 1 to measure bandwidth                                                                   |
| bgpMeasurements       | integer                   | 0 or 1                                                  | 1 to enable bgp measurements                                                             |
| createdBy             | string                    | Username (email@company.com)                            | User’s email                                                                             |
| createdDate           | string                    | YYYY-MM-DD HH:mm:ss formatted date                      | Shown in UTC                                                                             |
| enabled               | integer                   | 0 or 1                                                  | 1 to enable the test, 0 to disable the test                                              |
| interval              | integer                   | \[60, 120, 300, 600, 900, 1800, 3600]                   | Value in seconds                                                                         |
| modifiedBy            | string                    | Username (email@company.com)                            | User’s email                                                                             |
| modifiedDate          | string                    | YYYY-MM-DD HH:mm:ss formatted date                      | Shown in UTC                                                                             |
| mtuMeasurements       | integer                   | 0 or 1                                                  | 1 to measure MTU sizes on network tests                                                  |
| networkMeasurements   | integer                   | 0 or 1                                                  | 1 to perform network tests                                                               |
| port                  | integer                   | (1..65535)                                              | TCP port used to perform the test; if ICMP is selected, -1 is returned                   |
| protocol              | string                    | `TCP` or `ICMP`                                         | Protocol used to perform the test                                                        |
| savedEvent            | integer                   | 0 or 1                                                  | Indicates 1 for a saved event, 0 for a normal test                                       |
| server                | string                    | (any)                                                   | Target domain name or IP address                                                         |
| testId                | integer                   | Unique ID of test                                       | Each test is assigned a unique ID; this is used to access test data from other endpoints |
| testName              | string                    | (any)                                                   | Test name must be unique                                                                 |
| type                  | string                    | Type of test being queried                              | Test type is implicit in the test creation url                                           |
| usePublicBgp          | integer                   | 0 or 1                                                  | Use all the public BGP monitors                                                          |
| application           | string                    | WEBEX,MSTEAMS,ZOOM                                      | Which supported application to monitor                                                   |

[`POST /v6/endpoint-automated-session-tests/new` Creating an Automated Session Test](broken-reference)

Creates a new Endpoint Automated Session test in ThousandEyes, based on properties provided in the POST data. In order to create a new test, the user attempting the creation must be an Account Admin.

Regular users are blocked from using any of the POST-based methods.

#### Request <a href="#request" id="request"></a>

* Request body should contain fields to be set during creation.

**Example - AST test**

`$ curl -i https://api.thousandeyes.com/v6/endpoint-automated-session-tests/new.json \ -d '{ "flagPing": true, "flagTraceroute": true, "interval" : 3600, "maxMachines": 5, "application": "WEBEX", "labelIds": [1, 2, 3], "testName": "Network test" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

| Field          | Data Type        | Units                             | Notes                                                                                             |
| -------------- | ---------------- | --------------------------------- | ------------------------------------------------------------------------------------------------- |
| agentIds       | array of strings | n/a                               | List of agent ids. Must be set if agentSelectorType == SPECIFIC\_AGENTS                           |
| flagPing       | boolean          | n/a                               | Optional flag indicating if test should run ping. If not specified, true is used by default       |
| flagTraceroute | boolean          | n/a                               | Optional flag indicating if test should run traceroute. If not specified, true is used by default |
| interval       | integer          | \[120, 300, 600, 900, 1800, 3600] | Interval in seconds that the test will execute on                                                 |
| labelIds       | array of longs   | n/a                               | List of label ids. Must be set if agentSelectorType == LIST\_OF\_LABELS                           |
| maxMachines    | integer          | \[1-100000]                       | Maximum number of agents which can execute this test                                              |
| testName       | string           | n/a                               | Name of the test                                                                                  |
| application    | string           | n/a                               | monitored application, can be one of WEBEX, ZOOM, MSTEAMS                                         |

#### Response <a href="#response" id="response"></a>

If a test is successfully created, an HTTP/201 CREATED response will be returned, and the test definition will be returned. See the example below.

Response does not include the results of the test. Once the test has been run, results can be retrieved using [Endpoint Test Data](https://developer.thousandeyes.com/v6/endpoint\_test\_data) endpoints. API test data endpoints URLs are provided in test definition output upon test creation. See the example below.

`HTTP/1.1 201 Created Server: nginx Date: Mon, 17 Feb 2020 13:41:02 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1490622120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

**Body**

`{ "automatedSessionTests": [ { "createdDate": "2022-05-06 09:20:27", "modifiedDate": "2022-05-06 09:20:27", "createdBy": "API User (noprely@thousandeyes.com)", "modifiedBy": "API User (noprely@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 9918128, "testName": " . . .. . . .. ", "interval": 60, "subinterval": -1, "port": 443, "protocol": "ICMP", "networkMeasurements": 1, "mtuMeasurements": 0, "bandwidthMeasurements": 0, "bgpMeasurements": 0, "usePublicBgp": 0, "application": "WEBEX", "apiLinks": [ { "rel": "self", "href": "https://api.stg.thousandeyes.com/v6/endpoint-automated-session-tests/9918128" }, { "rel": "data", "href": "https://api.stg.thousandeyes.com/v6/endpoint-data/automated-session-tests/net/metrics/9918128" }, { "rel": "data", "href": "https://api.stg.thousandeyes.com/v6/endpoint-data/automated-session-tests/net/path-vis/9918128" } ] } ] }`
