# Labels

### Labels

[`GET /v6/groups` Labels list](broken-reference)

Returns a list of all labels (formerly called groups) configured in ThousandEyes. This includes both Agent and Test labels.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Response <a href="#response" id="response"></a>

Sends back an array of labels configured in the platform. Metadata of the response is returned according to the following table:

| Field   | Data Type | Units | Notes                                                                                                                                                                        |
| ------- | --------- | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name    | string    | n/a   | Name of the label                                                                                                                                                            |
| groupId | integer   | n/a   | Unique ID of the label; this number is negative for built-in labels. Query the `/groups/{id}` endpoint to see a list of agents/tests with this label.                        |
| type    | string    | n/a   | Either `tests`, `agents`, `endpoint_tests`, `endpoint_agents` or `dashboards`, indicates the type of label. To show only this label type, query the /groups/{type} endpoint. |
| builtin | integer   | n/a   | 1 for built-in labels, and 0 for user-created labels. Note that built-in labels are read-only.                                                                               |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/groups.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "groups": [ { "name": "Infrastructure tests", "groupId": 961, "type": "tests", "builtin": 0 }, { "name": "My label", "groupId": 714, "type": "agents", "builtin": 0 }, { "builtin": 1, "groupId": -8, "name": "Shared", "type": "tests" }, { "builtin": 0, "groupId": 25458, "name": "Endpoint label", "type": "endpoint_agents" }, { "builtin": 1, "groupId": -2, "name": "Cloud", "type": "agents" }, { "builtin": 1, "groupId": -3, "name": "IPv4 Compatible", "type": "agents" }, { "builtin": 1, "groupId": -4, "name": "IPv6 Compatible", "type": "agents" }, { "builtin": 1, "groupId": -5, "name": "Proxied", "type": "agents" }, { "builtin": 1, "groupId": -6, "name": "Enterprise Cluster", "type": "agents" }, { "builtin": 1, "groupId": -1, "name": "Enterprise", "type": "agents" }, { "builtin": 0, "groupId": 123, "name": "Dashboard Label", "type": "dashboards" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/groups/{type}` Labels list by type](broken-reference)

Returns a list of all tests of the label (formerly called group) type specified, configured in ThousandEyes.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{type}` corresponds to the following options:
  * `agents`
  * `tests`
  * `endpoint-agents`
  * `endpoint-tests`
  * `dashboards`
* no request body

#### Response <a href="#response" id="response"></a>

Sends back an array of labels configured for the type specified in the platform. Metadata of the response is returned according to the following table:

| Field   | Data Type | Units | Notes                                                                                                                                                 |
| ------- | --------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| name    | string    | n/a   | Name of the label                                                                                                                                     |
| groupId | integer   | n/a   | Unique ID of the label; this number is negative for built-in labels. Query the `/groups/{id}` endpoint to see a list of agents/tests with this label. |
| type    | string    | n/a   | Either `tests`, `agents`, `endpoint_tests`, `endpoint_agents` or `dashboards`, indicates the type of label.                                           |
| builtin | integer   | n/a   | 1 for built-in labels, and 0 for user-created labels. Note that built-in labels are read-only.                                                        |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/groups/tests.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "groups": [ { "name": "Infrastructure tests", "groupId": 961, "type": "tests", "builtin": 0 }, { "builtin": 1, "groupId": -8, "name": "Shared", "type": "tests" }, { "builtin": 1, "groupId": -9, "name": "Saved Event", "type": "tests" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/groups/{groupId}` Label details](broken-reference)

Returns details for a label (formerly called group) configured in ThousandEyes.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{groupId}` the ID of the label to retrieve
* no request body

#### Response <a href="#response" id="response"></a>

Returns the label details. Metadata of the response is returned according to the following table:

| Field          | Data Type                       | Units | Notes                                                                                                                                                                    |
| -------------- | ------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name           | string                          | n/a   | Name of the label                                                                                                                                                        |
| groupId        | integer                         | n/a   | Unique ID of the label; this number is negative for built-in labels. Query the `/groups/{id}` endpoint to see a list of agents/tests with this label.                    |
| type           | string                          | n/a   | Either `tests`, `agents`, `endpoint_tests`, `endpoint_agents` or `dashboards`, indicates the type of label.                                                              |
| builtin        | integer                         | n/a   | 1 for built-in labels, and 0 for user-created labels. Note that built-in labels are read-only.                                                                           |
| agents         | array of agent objects          | n/a   | Agent objects are shown for an `agents` type label only. See [Agent Metadata](https://developer.thousandeyes.com/v6/agents/#/agentid) for more details on agent objects. |
| tests          | array of test objects           | n/a   | Test objects are shown for a `tests` type label only. See [Test Metadata](https://developer.thousandeyes.com/v6/tests/#/test\_metadata) for more detail on test objects. |
| endpointAgents | array of endpoint agent objects | n/a   | Populated for Endpoint agent labels.                                                                                                                                     |
| endpointTests  | array of endpoint test objects  | n/a   | Populated for Endpoint test labels.                                                                                                                                      |
| dashboardIds   | array of dashboardIds           | n/a   | Populated for Dashboard labels.                                                                                                                                          |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/groups/-2.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "groups": [ { "name": "Cloud", "groupId": -2, "type": "agents", "builtin": 1, "agents": [ { "agentId": 3, "agentName": "Singapore", "agentType": "Cloud", "countryId": "SG", "ipAddresses": [ "202.150.211.165", "202.150.211.164", "202.150.211.163" ], "ipv6Policy": "FORCE_IPV4", "location": "Singapore" } ... ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/groups/{type}/{groupId}` Label details (by label type)](broken-reference)

Returns a list of all labels (formerly called groups) configured in ThousandEyes. This includes both Agent and Test labels.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{type}` corresponds to the following options:
  * `agents`
  * `tests`
  * `endpoint-agents`
  * `endpoint-tests`
  * `dashboards`
* `{groupId}` the ID of the label to retrieve
* no request body

#### Response <a href="#response" id="response"></a>

Returns the label details. Metadata of the response is returned according to the following table:

| Field          | Data Type                       | Units | Notes                                                                                                                                                                    |
| -------------- | ------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name           | string                          | n/a   | Name of the label                                                                                                                                                        |
| groupId        | integer                         | n/a   | Unique ID of the label; this number is negative for built-in labels. Query the `/groups/{id}` endpoint to see a list of agents/tests with this label.                    |
| type           | string                          | n/a   | Either `tests`, `agents`, `endpoint_tests`, `endpoint_agents` or `dashboards`, indicates the type of label requested.                                                    |
| builtin        | integer                         | n/a   | 1 for built-in labels, and 0 for user-created labels. Note that built-in labels are read-only.                                                                           |
| agents         | array of agent objects          | n/a   | Agent objects are shown for an `agents` type label only. See [Agent Metadata](https://developer.thousandeyes.com/v6/agents/#/agentid) for more details on agent objects. |
| tests          | array of test objects           | n/a   | Test objects are shown for a `tests` type label only. See [Test Metadata](https://developer.thousandeyes.com/v6/tests/#/test\_metadata) for more detail on test objects. |
| endpointAgents | array of endpoint agent objects | n/a   | Populated for Endpoint agent labels.                                                                                                                                     |
| endpointTests  | array of endpoint test objects  | n/a   | Populated for Endpoint test labels.                                                                                                                                      |
| dashboardIds   | array of dashboardIds           | n/a   | Populated for Dashboard labels.                                                                                                                                          |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/groups/agents/-2.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "groups": [ { "name": "Cloud", "groupId": -2, "type": "agents", "builtin": 1, "agents": [ { "agentId": 3, "agentName": "Singapore", "agentType": "Cloud", "countryId": "SG", "ipAddresses": [ "202.150.211.165", "202.150.211.164", "202.150.211.163" ], "ipv6Policy": "FORCE_IPV4", "location": "Singapore" } ... ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/groups/{type}/new` Creating a label](broken-reference)

Creates a new label (formerly called group) in ThousandEyes, based on properties provided in the POST data. In order to create a new label, the user attempting the creation must have sufficient privileges to create labels.

Regular users are blocked from using any of the POST-based methods.

Note: When creating or updating a label and assigning agents or tests, the user needs permission to modify the objects being added.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{type}` corresponds to the following options:
  * `agents`
  * `tests`
  * `endpoint-agents`
  * `dashboards`
* POST body includes the following:
  * `name` the name of the new label - this must be unique.
  * `tests` an array of testId objects, if the `type` specified is tests
  * `agents` an array of agentId objects, if the `type` specified is agents
  * `endpointAgents` an array of agentId objects, if the `type` specified is endpoint-agents
  * `dashboards` an array of dashboardIds, if the `type` specified is dashboards

See the example below for POST body syntax

#### Response <a href="#response" id="response"></a>

If successful, sends back an HTTP/201 CREATED response code, and the new object metadata (just as if you’d called `/groups/{id}` with the new label ID). Metadata per the following table:

| Field          | Data Type                       | Units | Notes                                                                                                                                                                    |
| -------------- | ------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name           | string                          | n/a   | Name of the label                                                                                                                                                        |
| groupId        | integer                         | n/a   | Unique ID of the label; this number is negative for built-in labels. Query the `/groups/{id}` endpoint to see a list of agents/tests with this label.                    |
| type           | string                          | n/a   | Either `tests`, `agents`, `endpoint_agents` or `dashboards`, indicates the type of label.                                                                                |
| builtin        | integer                         | n/a   | 1 for built-in labels, and 0 for user-created labels. Note that built-in labels are read-only.                                                                           |
| agents         | array of agent objects          | n/a   | Agent objects are shown for an `agents` type label only. See [Agent Metadata](https://developer.thousandeyes.com/v6/agents/#/agentid) for more details on agent objects. |
| tests          | array of test objects           | n/a   | Test objects are shown for a `tests` type label only. See [Test Metadata](https://developer.thousandeyes.com/v6/tests/#/test\_metadata) for more detail on test objects. |
| endpointAgents | array of endpoint agent objects | n/a   | Endpoint agent objects are shown for an `endpoint_agents` type label only.                                                                                               |
| dashboardIds   | array of dashboardIds           | n/a   | Dashboard Ids are shown for a `dashboards` type label only.                                                                                                              |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/groups/tests/new \ -d '{ "name": "Dave's new group", "tests": [ {"testId": 5048}, {"testId": 6600} ] }' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 201 CREATED Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "groups": [ { "name": "Dave's new group", "groupId": 1374, "type": "tests", "builtin": 0, "tests": [ { "createdDate": "2014-06-13 04:01:07", "modifiedDate": "2015-01-06 19:27:03", "createdBy": "Dave Fraleigh (dave@thousandeyes.com)", "modifiedBy": "Dave Fraleigh (dave@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 6600, "testName": "Bozo BGP test 1", "type": "bgp", "prefix": "38.122.0.0/16", "alertsEnabled": 0, "liveShare": 0, "includeCoveredPrefixes": 0, "apiLinks": [...] }, { "createdDate": "2014-03-18 20:05:03", "modifiedDate": "2015-07-31 17:20:54", "createdBy": "Dave Fraleigh (dave@thousandeyes.com)", "modifiedBy": "Dave Fraleigh (dave@thousandeyes.com)", "enabled": 0, "savedEvent": 0, "testId": 5048, "testName": "www.yahoo.com A", "type": "dns-server", "interval": 300, "domain": "www.yahoo.com A", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "alertsEnabled": 0, "liveShare": 0, "recursiveQueries": 1, "dnsServers": [...], "apiLinks": [...] } ] } ] }`

**Body - Endpoint agents**

`{ "name":"Label name", "endpointAgents": [ { "agentId": "1b06b773-0438-426e-a843-31a6f86b2cc2" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/groups/{groupId}/update` Updating a label](broken-reference)

Updates a label (formerly called group) in ThousandEyes, based on properties provided in the POST data. In order to edit a label, the user must have access to the target label, and have access to modify the objects that the label contains. For example, to update an agent label, the user needs the Edit Agents permission assigned to their role.

Regular users are blocked from using any of the POST-based methods.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `groupId` the label that you wish to update, found in either the `/groups` or the `/groups/{type}` endpoint.

#### Response <a href="#response" id="response"></a>

Returns the label details, following update. Metadata of the response is returned according to the following table:

| Field          | Data Type                       | Units | Notes                                                                                                                                                                    |
| -------------- | ------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name           | string                          | n/a   | Name of the label                                                                                                                                                        |
| groupId        | integer                         | n/a   | Unique ID of the label; this number is negative for built-in labels. Query the `/groups/{id}` endpoint to see a list of agents/tests with this label.                    |
| type           | string                          | n/a   | Either `tests`, `agents`, `endpoint_agents` or `dashboards`, indicates the type of label.                                                                                |
| builtin        | integer                         | n/a   | 1 for built-in labels, and 0 for user-created labels. Note that built-in labels are read-only.                                                                           |
| agents         | array of agent objects          | n/a   | Agent objects are shown for an `agents` type label only. See [Agent Metadata](https://developer.thousandeyes.com/v6/agents/#/agentid) for more details on agent objects. |
| tests          | array of test objects           | n/a   | Test objects are shown for a `tests` type label only. See [Test Metadata](https://developer.thousandeyes.com/v6/tests/#/test\_metadata) for more detail on test objects. |
| endpointAgents | array of endpoint agent objects | n/a   | Endpoint agent objects are shown for an `endpoint_agents` type label only.                                                                                               |
| dashboardIds   | array of dashboardIds           | n/a   | Dashboard Ids are shown for a `dashboards` type label only.                                                                                                              |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/groups/1356/update \ -d '{ "name": "Dave's new group", "tests": [ {"testId": 5048 }, {"testId": 6600 } ] }' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "groups": [ { "name": "Dave's new group", "groupId": 1356, "type": "tests", "builtin": 0, "tests": [ { "createdDate": "2014-06-13 04:01:07", "modifiedDate": "2015-01-06 19:27:03", "createdBy": "Dave Fraleigh (dave@thousandeyes.com)", "modifiedBy": "Dave Fraleigh (dave@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 6600, "testName": "Bozo BGP test 1", "type": "bgp", "prefix": "38.122.0.0/16", "alertsEnabled": 0, "liveShare": 0, "includeCoveredPrefixes": 0, "apiLinks": [...] }, { "createdDate": "2014-03-18 20:05:03", "modifiedDate": "2015-07-31 17:20:54", "createdBy": "Dave Fraleigh (dave@thousandeyes.com)", "modifiedBy": "Dave Fraleigh (dave@thousandeyes.com)", "enabled": 0, "savedEvent": 0, "testId": 5048, "testName": "www.yahoo.com A", "type": "dns-server", "interval": 300, "domain": "www.yahoo.com A", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "alertsEnabled": 0, "liveShare": 0, "recursiveQueries": 1, "dnsServers": [...], "apiLinks": [...] } ] } ] }`

**Body - Endpoint agents**

`{ "name":"Label name", "endpointAgents": [ { "agentId": "1b06b773-0438-426e-a843-31a6f86b2cc2" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/groups/{groupId}/delete` Deleting a label](broken-reference)

Deletes a label (formerly called group) currently configured in ThousandEyes. Note that built-in labels (with negative `groupId` numbers) are not eligible for deletion.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `groupId` the label that you wish to delete, found in either the `/groups` or the `/groups/{type}` endpoint.
* No request body

#### Response <a href="#response" id="response"></a>

Returns an `HTTP/204 NO CONTENT` response.

#### Example <a href="#example" id="example"></a>

`$ curl -i https://api.thousandeyes.com/v6/groups/1356/delete \ -d '' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 204 NO CONTENT Server: nginx Date: Tue, 15 Mar 2016 00:20:26 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1493730300 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

* The body of a delete request will be empty.

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
