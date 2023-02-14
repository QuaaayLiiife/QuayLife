# Test Data

### Test Data

[`GET /v6/net/metrics/{testId}` (Network) End-to-End metrics](broken-reference)

Returns network metrics (loss, latency, jitter, and bandwidth) from each agent, for each _roundId_ in the requested window. A **time frame** must be specified, or the current round of data will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `direction=[FROM_TARGET, TO_TARGET, BIDIRECTIONAL]` Applicable only for bidirectional Agent-to-Agent tests, specifies the direction for the metrics being retrieved. In the case of bidirectional data, the aggregated data is returned, otherwise unidirectional data will be returned. In the case of unidirectional tests queried with an invalid direction parameter, an error response will be thrown.

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field      | Data Type | Units        | Notes                                                       |
| ---------- | --------- | ------------ | ----------------------------------------------------------- |
| agentId    | integer   | n/a          | unique ID of agent, from `/agents` endpoint                 |
| agentName  | string    | n/a          | display name of the agent responding                        |
| countryId  | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                |
| date       | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                 |
| roundId    | long      | seconds      | epoch time (seconds) indicating the start time of the round |
| permalink  | url       | n/a          | link to jump to this result in the front end                |
| serverIp   | string    | n/a          | ip of target server                                         |
| server     | url       | n/a          | target server, including port (if method used is TCP)       |
| loss       | float     | percentage   | % of packets not reaching destination                       |
| minLatency | float     | milliseconds | minimum RTT for packets sent to destination                 |
| maxLatency | float     | milliseconds | maximum RTT for packets sent to destination                 |
| avgLatency | float     | milliseconds | average RTT for packets sent to destination                 |
| jitter     | float     | milliseconds | standard deviation of latency                               |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/net/metrics/817.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 08 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493231280 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "net": { "test": { "enabled": 1, "testId": 817, "testName": "http://www.thousandeyes.com", "type": "http-server", "interval": 900, "url": "http://www.thousandeyes.com", "modifiedDate": "2013-05-11 02:02:21", "networkMeasurements": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "apiLinks": [...] }, "metrics": [ { "agentName": "Hong Kong", "countryId": "HK", "date": "2013-11-13 02:33:05", "serverIp": "50.18.127.223", "loss": 0.0, "permalink": "https://app.thousandeyes.com/net/metrics?__a=75&testId=817&roundId=1384309800&serverId=71&agentId=12", "agentId": 12, "server": "www.thousandeyes.com:80", "roundId": 1384309800 "minLatency": 167.0, "avgLatency": 167.04, "maxLatency": 168.0, "jitter": 0.076808 }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/net/path-vis/{testId}` (Network) Path visualization](broken-reference)

Returns a summary of the path visualization data collected from each agent to the destination. In each path visualization attempt, three attempts are made to reach the destination. Each set of data is summarized, based on response time, number of hops, and response time to the target. A **time frame** must be specified, or the current round of data will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `direction=[FROM_TARGET, TO_TARGET]` Applicable only for bidirectional Agent-to-Agent tests, specifies the direction for the metrics being retrieved. If available, bidirectional data is returned by default.

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field                  | Data Type | Units   | Notes                                                                         |
| ---------------------- | --------- | ------- | ----------------------------------------------------------------------------- |
| agentId                | integer   | n/a     | unique ID of agent, from `/agents` endpoint                                   |
| agentName              | string    | n/a     | display name of the agent responding                                          |
| countryId              | string    | n/a     | ISO-3166-1 alpha-2 country code of the agent                                  |
| date                   | dateTime  | n/a     | yyyy-MM-dd hh:mm:ss, in UTC                                                   |
| roundId                | long      | seconds | epoch time (seconds) indicating the start time of the round                   |
| permalink              | url       | n/a     | link to jump to this result in the front end                                  |
| server                 | url       | n/a     | target server, including port (if method used is TCP)                         |
| serverIp               | string    | n/a     | ip address of target server                                                   |
| sourceIp               | string    | n/a     | ip address of source agent                                                    |
| sourcePrefix           | string    | n/a     | ip prefix of source agent                                                     |
| endpoints              | array     | n/a     | shows all iterations of path trace, with each iteration specified by a pathId |
| endpoints.numberOfHops | integer   | n/a     | number of hops for path trace to destination                                  |
| endpoints.ipAddress    | string    | n/a     | destination                                                                   |
| endpoints.pathId       | string    | n/a     | unique ID of path trace                                                       |
| endpoints.responseTime | integer   | n/a     | RTT of the path trace to the destination                                      |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/net/path-vis/817.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 26 Apr 2017 18:31:00 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 234 X-Organization-Rate-Limit-Reset: 1493231520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "net": { "test": { "enabled": 1, "testId": 817, "testName": "http://www.thousandeyes.com", "type": "http-server", "interval": 900, "url": "http://www.thousandeyes.com", "modifiedDate": "2013-05-11 02:02:21", "networkMeasurements": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "apiLinks": [...] }, "pathVis": [ { "agentName": "Hong Kong", "countryId": "HK", "date": "2013-11-13 02:47:46", "server": "www.thousandeyes.com:80", "serverIp": "50.18.127.223", "sourceIp": "123.103.248.179", "sourcePrefix": "123.103.248.0/24", "permalink": "https://app.thousandeyes.com/net/path-vis?__a=75&testId=817&roundId=1384310700&serverId=71&agentId=12", "agentId": 12, "endpoints": [ { "numberOfHops": 16, "ipAddress": "50.18.127.223", "responseTime": 167, "pathId": "6537222451557817610263112715264" }, { "numberOfHops": 16, "ipAddress": "50.18.127.223", "responseTime": 167, "pathId": "6537222451557817610263112715265" }, { "numberOfHops": 16, "ipAddress": "50.18.127.223", "responseTime": 167, "pathId": "6537222451557817610263112715266" } ], "roundId": 1384310700 }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/net/path-vis/{testId}/{agentId}/{roundId}` (Network) Detailed path trace](broken-reference)

Returns a hop-by-hop summary of the path trace data collected during path visualization. In each path visualization attempt, three attempts are made to reach the destination, and the entire path will be shown in sequence. A roundId must be specified. For agent-to-agent tests, there’s a special case to consider, since the test can be bidirectional.

Consider agents A, B and C testing agent D, on a bidirectional basis. To query for the route from agent A to agent D, query with testId/{agentA}/roundId?direction=TO\_TARGET. For the path from D to A, query with testId/{agentA}/roundId?direction=FROM\_TARGET. To get both paths, query the same endpoint with direction=BIDIRECTIONAL. In all cases, the source field will reflect agent A, and the destination field will reflect agent D, but the direction field will show the direction of the trace.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

Required parameters:

* `{testId}` the ID of the test you wish to retrieve
* `{agentId}` the ID of the agent from which you wish to obtain data
* `{roundId}` the round ID for which you wish to obtain data. Equals the beginning of the testing round, in epoch time format.
* There is no request body for this request.

Optional request parameter:

* `direction=[TO_TARGET, FROM_TARGET, BIDIRECTIONAL]` indicates the direction of a path trace in the case of a bidirectional agent-to-agent test. This parameter is only applied in the case of bidirectional agent-to-agent tests. Specify the value on the querystring. Without specifying the field, the test will use the default direction for the test, which is chosen based on the following list:
  * BIDIRECTIONAL (shows both TO\_TARGET and FROM\_TARGET directions)
  * TO\_TARGET (shows path from source agent to target agent)
  * FROM\_TARGET (shows path from target agent to source agent)

#### Response <a href="#response" id="response"></a>

* Each route should start with a hop of 1
* Where a hop number is missing from response data, this is an indication that a star (\*) response was returned in the path trace attempt for that hop.

| Field                   | Data Type | Units        | Notes                                                                                                                             |
| ----------------------- | --------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| agentId                 | integer   | n/a          | unique ID of agent, from `/agents` endpoint                                                                                       |
| agentName               | string    | n/a          | display name of the agent responding                                                                                              |
| countryId               | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                                                                                      |
| date                    | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                                                                                       |
| direction               | string    | n/a          | direction of the trace results. Can be \[TO\_TARGET, FROM\_TARGET]. This field is only shown in the case of Agent to Agent tests. |
| roundId                 | long      | seconds      | epoch time (seconds) indicating the start time of the round                                                                       |
| permalink               | url       | n/a          | link to jump to this result in the front end                                                                                      |
| server                  | url       | n/a          | target server, including port (if method used is TCP)                                                                             |
| serverIp                | string    | n/a          | ip address of target server                                                                                                       |
| sourceIp                | string    | n/a          | ip address of source agent                                                                                                        |
| sourcePrefix            | string    | n/a          | ip prefix of source agent                                                                                                         |
| routes                  | array     | n/a          | shows 3 iterations of path trace, with each iteration specified by a pathId                                                       |
| routes.pathId           | string    | n/a          | unique ID of path trace                                                                                                           |
| routes.hops             | array     | n/a          | array of hop objects indicating each step in the traceroute                                                                       |
| routes.hops.hop         | integer   | n/a          | index of hop                                                                                                                      |
| routes.hops.ipAddress   | string    | n/a          | IP address of the hop                                                                                                             |
| routes.hop.prefix       | string    | n/a          | Prefix of IP address shown in CIDR                                                                                                |
| routes.hop.rdns         | string    | n/a          | reverse DNS entry of IP, if available                                                                                             |
| routes.hop.network      | string    | n/a          | Autonomous System originating the prefix                                                                                          |
| routes.hop.responseTime | integer   | milliseconds | RTT to the hop’s IP                                                                                                               |
| routes.hop.location     | string    | n/a          | location information for the hop                                                                                                  |
| routes.hop.mpls         | string    | n/a          | Multiprotocol Label Switching information, if available                                                                           |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/net/path-vis/817/146/1383887700.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 07 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493233740 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "net": { "test": { "enabled": 1, "testId": 817, "testName": "http://www.thousandeyes.com", "type": "http-server", "interval": 900, "url": "http://www.thousandeyes.com", "modifiedDate": "2013-05-11 02:02:21", "networkMeasurements": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "apiLinks": [...] }, "pathVis": [ { "agentName": "San Jose, CA", "countryId": "US", "date": "2013-11-08 05:15:12", "server": "www.thousandeyes.com:80", "serverIp": "50.18.127.223", "sourceIp": "198.89.98.67", "sourcePrefix": "198.89.96.0/19", "routes": [ { "pathId": "6535224890535563750337719341569", "hops": [ { "hop": 4, "ipAddress": "154.54.84.53", "prefix": "154.48.0.0/12", "rdns": "te0-2-0-4.ccr21.sjc01.atlas.cogentco.com", "network": "Cogent Communications (AS 174)", "responseTime": 2, "location": "San Francisco Area" }, { "hop": 5, "ipAddress": "154.54.6.106", "prefix": "154.48.0.0/12", "rdns": "be2000.ccr21.sjc03.atlas.cogentco.com", "network": "Cogent Communications (AS 174)", "responseTime": 1, "location": "San Francisco Area" }, { "hop": 6, "ipAddress": "154.54.13.126", "prefix": "154.48.0.0/12", "rdns": "verio.sjc03.atlas.cogentco.com", "network": "Cogent Communications (AS 174)", "responseTime": 1, "location": "San Francisco Area" }, { "hop": 7, "ipAddress": "129.250.4.118", "prefix": "129.250.0.0/16", "rdns": "ae-4.r06.plalca01.us.bb.gin.ntt.net", "network": "NTT America, Inc. (AS 2914)", "responseTime": 2, "location": "San Francisco Area", "mpls": "L=399088,E=0,S=1,T=1" }, { "hop": 8, "ipAddress": "140.174.21.182", "prefix": "140.174.0.0/16", "rdns": "ae-1.amazon.plalca01.us.bb.gin.ntt.net", "network": "NTT America, Inc. (AS 2914)", "responseTime": 2, "location": "San Francisco Area" }, { "hop": 9, "ipAddress": "205.251.229.46", "prefix": "205.251.228.0/22", "network": "Amazon.com, Inc. (AS 16509)", "responseTime": 4, "location": "Seattle Area" }, { "hop": 10, "ipAddress": "72.21.222.19", "prefix": "72.21.220.0/22", "network": "Amazon.com, Inc. (AS 16509)", "responseTime": 3, "location": "Seattle Area" }, { "hop": 11, "ipAddress": "216.182.236.109", "prefix": "216.182.232.0/21", "network": "Amazon.com, Inc. (AS 14618)", "responseTime": 4, "location": "Seattle Area" }, { "hop": 16, "ipAddress": "50.18.127.223", "prefix": "50.18.64.0/18", "rdns": "ec2-50-18-127-223.us-west-1.compute.amazonaws.com", "network": "Amazon.com, Inc. (AS 16509)", "responseTime": 4, "location": "San Francisco Area" } ] }, { "pathId": "6535224890535563750337719341568", "hops": [...] }, { "pathId": "6535224890535563750337719341570", "hops": [...] } ], "permalink": "https://app.thousandeyes.com/net/path-vis?__a=75&testId=817&roundId=1383887700&serverId=71&agentId=146", "agentId": 146, "roundId": 1383887700 } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/net/bgp-metrics/{testId}` (Network) BGP metrics](broken-reference)

Returns a list of BGP monitors observing the target prefix of the destination, and returns the prefix, AS Number, and reachability, path updates, and path changes for the target network.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test for which BGP data is of interest
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

* **Note:** Monitors are not agents. Not all agents are in a network being monitored, and not all monitors have associated agents.

| Field        | Data Type | Units      | Notes                                                              |
| ------------ | --------- | ---------- | ------------------------------------------------------------------ |
| monitorId    | integer   | n/a        | unique ID of monitor, from `/bgp-monitors` endpoint                |
| monitorName  | string    | n/a        | display name used for the monitor                                  |
| countryId    | string    | n/a        | ISO-3166-1 alpha-2 country code of the agent                       |
| date         | dateTime  | n/a        | yyyy-MM-dd hh:mm:ss, in UTC                                        |
| roundId      | long      | seconds    | epoch time (seconds) indicating the start time of the round        |
| permalink    | url       | n/a        | link to jump to this result in the front end                       |
| prefixId     | integer   | n/a        | internally tracked prefix ID                                       |
| prefix       | string    | n/a        | prefix being tracked                                               |
| updates      | float     | n/a        | number of updates tracked against this prefix by this monitor      |
| pathChanges  | float     | n/a        | number of path changes tracked against this prefix by this monitor |
| reachability | float     | percentage | percentage reachability                                            |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/net/bgp-metrics/817.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 07 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493233860 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "net": { "test": { "enabled": 1, "testId": 817, "testName": "http://www.thousandeyes.com", "type": "http-server", "interval": 900, "url": "http://www.thousandeyes.com", "modifiedDate": "2013-05-11 02:02:21", "networkMeasurements": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "apiLinks": [...] }, "bgpMetrics": [ { "countryId": "CA", "date": "2013-11-13 03:45:00", "prefixId": 215, "prefix": "50.16.0.0/14", "monitorName": "Vancouver, Canada - Bell Canada (AS 6539)", "monitorId": 45, "reachability": 100, "roundId": 1384314300, "updates": 0.0, "permalink": "https://app.thousandeyes.com/net/bgp-vis?__a=75&testId=817&roundId=1384314300&prefixId=215", "pathChanges": 0.0 }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/net/bgp-routes/{testId}/{prefixId}/{roundId}` (Network) BGP route information](broken-reference)

Returns a sequenced list of networks transited for a specific network prefix. Shows a list of monitors assigned to the test, and the paths transited to reach the destination. This is analogous to showing the ASPath information from a BGP Routing Information Base (rib) dump.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test for which BGP data is of interest
* `{prefixId}` the ID of the prefix in question. Obtain prefixId from the `/net/bgp-metrics/{testId}` endpoint
* `{roundId}` the round for which you wish to obtain data. Obtain roundId from the `/net/bgp-metrics/{testId}` endpoint
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

* **Note:** Monitors are not agents. Not all agents are in a network being monitored, and not all monitors have associated agents.

| Field       | Data Type | Units   | Notes                                                                                                                                                                                                                                                                                                                     |
| ----------- | --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| monitorId   | integer   | n/a     | unique ID of monitor, from `/bgp-monitors` endpoint                                                                                                                                                                                                                                                                       |
| monitorName | string    | n/a     | display name used for the monitor                                                                                                                                                                                                                                                                                         |
| countryId   | string    | n/a     | ISO-3166-1 alpha-2 country code of the agent                                                                                                                                                                                                                                                                              |
| date        | dateTime  | n/a     | yyyy-MM-dd hh:mm:ss, in UTC                                                                                                                                                                                                                                                                                               |
| roundId     | long      | seconds | epoch time (seconds) indicating the start time of the round                                                                                                                                                                                                                                                               |
| permalink   | url       | n/a     | link to jump to this result in the front end                                                                                                                                                                                                                                                                              |
| prefixId    | integer   | n/a     | internally tracked prefix ID                                                                                                                                                                                                                                                                                              |
| prefix      | string    | n/a     | prefix being tracked                                                                                                                                                                                                                                                                                                      |
| active      | boolean   | n/a     | 1 for an active route, 0 for an inactive route. An inactive route was an active route in the previous test round and is now superseded by another active (preferred) route. When requesting data for the test round in which a route change happened, both routes (active and inactive one) are included in the response. |
| hops        | array     | n/a     | see below for individual hop fields                                                                                                                                                                                                                                                                                       |
| hops.asn    | integer   | n/a     | ASN of transit autonomous system                                                                                                                                                                                                                                                                                          |
| hops.asName | string    | n/a     | name of autonomous system                                                                                                                                                                                                                                                                                                 |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/net/bgp-routes/1137/27/1413225900.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 07 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493233860 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "net": { "test": { "enabled": 1, "savedEvent": 0, "testId": 1137, "testName": "Agents up?", "type": "network", "interval": 300, "server": "www.google.com:80", "protocol": "TCP", "networkMeasurements": 1, "mtuMeasurements": 0, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "alertsEnabled": 0, "liveShare": 0, "createdDate": "2013-03-06 18:07:51", "modifiedDate": "2014-10-13 18:17:53", "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "apiLinks": [...] }, "bgpRoutes": [ { "countryId": "CA", "date": "2014-10-13 18:45:00", "monitorId": 15, "monitorName": "Calgary, Canada - Telus (AS 852)", "prefixId": 27, "prefix": "74.125.0.0/16", "active": 1, "roundId": 1413225900, "hops": [ { "asn": 852, "asName": "Telus Advanced Communications" }, { "asn": 15169, "asName": "Google Inc." } ], "permalink": "https://app.thousandeyes.com/net/bgp-vis?__a=11&testId=1137&roundId=1413225900&agentId=null" }, ... ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/http-server/{testId}` (Web) HTTP server](broken-reference)

Returns response code, response and fetch times, TLS session details and component-level (DNS, Connect, Wait, Receive and Fetch) timing for the load of an object over HTTP.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `headers=1` optional, will output request and response header information in output. Example below assumes headers=1 was specified as an optional parameter.
* `certificates=1` output list of certificates in the certificate chain. Example below includes certificates=1 as a parameter.

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the HTTP Server (or page load) test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field           | Data Type        | Units            | Notes                                                                 |
| --------------- | ---------------- | ---------------- | --------------------------------------------------------------------- |
| agentId         | integer          | n/a              | unique ID of agent, from `/agents` endpoint                           |
| agentName       | string           | n/a              | display name of the agent responding                                  |
| countryId       | string           | n/a              | ISO-3166-1 alpha-2 country code of the agent                          |
| date            | dateTime         | n/a              | yyyy-MM-dd hh:mm:ss, in UTC                                           |
| roundId         | long             | seconds          | epoch time (seconds) indicating the start time of the round           |
| permalink       | url              | n/a              | link to jump to this result in the front end                          |
| serverIp        | string           | n/a              | IP address of destination server                                      |
| responseCode    | integer          | n/a              | code of HTTP response                                                 |
| numRedirects    | integer          | n/a              | number of redirects                                                   |
| redirectTime    | integer          | milliseconds     | cumulative redirect timing                                            |
| dnsTime         | integer          | milliseconds     | time required to resolve DNS                                          |
| sslTime         | integer          | milliseconds     | time to negotiate SSL/TLS                                             |
| connectTime     | integer          | milliseconds     | time required to establish a TCP connection to the server             |
| waitTime        | integer          | milliseconds     | time elapsed between completion of request and first byte of response |
| receiveTime     | integer          | milliseconds     | elapsed time between first and last byte of response                  |
| wireSize        | float            | bytes            | size of content, in bytes                                             |
| responseTime    | integer          | milliseconds     | time to first byte                                                    |
| throughput      | integer          | bytes per second | `wireSize` divided by `receiveTime`                                   |
| totalTime       | integer          | milliseconds     | response time + receive time                                          |
| requestHeaders  | string           | n/a              | crlf-delimited list of request headers in header: value format        |
| responseHeaders | string           | n/a              | crlf-delimited list of response headers in header: value format       |
| errorType       | string           | n/a              | type of error encountered; corresponds to phase of connection         |
| errorDetails    | string           | n/a              | error details, if an error were encountered                           |
| sslCipher       | string           | n/a              | cipher suite                                                          |
| sslVersion      | string           | n/a              | TLS version                                                           |
| sslCerts        | array of records | n/a              | list of certificates in the chain                                     |

If the optional parameter `certificates=1` is included in the request URL, the `sslCerts` field is added to the response and contains an array of objects each containing the following information:

| Field                         | Data Type        | Units | Notes                                                                                                                                                                        |
| ----------------------------- | ---------------- | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| daysUntilExpiry               | integer          | day   | days until certificate expires, rounded down. 0 is shown if there are less than 24 hours remaining. Calculated when the test was executed.                                   |
| fetchDateInValidCertDateRange | boolean          | n/a   | `true` when certificate fetch date is within the valid certificate date range, `false` otherwise                                                                             |
| hasValidSigningCert           | boolean          | n/a   | this field is implicitly `true`; it is output only when `false`. `false` indicates this certificate was missing a valid signing certificate in the chain.                    |
| issuerName                    | string           | n/a   | certificate issuer                                                                                                                                                           |
| notValidAfter                 | dateTime         | n/a   | yyyy-MM-dd hh:mm:ss, in UTC                                                                                                                                                  |
| notValidBefore                | dateTime         | n/a   | yyyy-MM-dd hh:mm:ss, in UTC                                                                                                                                                  |
| subjectAltNames               | array of strings | n/a   | alternative name(s) of the certificate subject, extracted from the Subject Alternative Name (SAN) X.509 certificate extension, for example `example.com`, `www2.example.com` |
| subjectName                   | string           | n/a   | certificate’s subject name - a value of the common name (CN) RDN from the certificate’s `Subject` attribute, for example `www.example.com`                                   |

#### Example <a href="#example" id="example"></a>

`$ curl "https://api.thousandeyes.com/v6/web/http-server/817.json?headers=1&certificates=1" \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Mon, 04 May 2020 17:09:30 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: ddg8s Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1588612200 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "pages": { "current": 1 }, "web": { "httpServer": [ { "agentId": 53279, "agentName": "San Jose, CA (CenturyLink)", "connectTime": 2, "countryId": "US", "date": "2020-05-04 16:15:14", "dnsTime": 0, "errorType": "None", "numRedirects": 1, "permalink": "https://app.thousandeyes.com/web/http-server?__a=75&testId=817&roundId=1588608900&agentId=53279", "receiveTime": 1, "redirectTime": 10, "requestHeaders": "GET / HTTP/1.1\r\nHost: www.thousandeyes.com\r\nUser-Agent: curl/7.58.0-DEV\r\nAccept: */*\r\nAccept-Encoding: deflate, gzip\r\nX-ThousandEyes-Agent: yes\r\n", "responseCode": 200, "responseHeaders": "HTTP/1.1 200 OK\r\nContent-Type: text/html;charset=UTF-8\r\nContent-Length: 9993\r\nConnection: keep-alive\r\nDate: Mon, 04 May 2020 16:13:00 GMT\r\nServer: Apache\r\nContent-Language: en-US\r\nContent-Encoding: gzip\r\nX-Frame-Options: sameorigin\r\nCache-Control: max-age=600, must-revalidate\r\nStrict-Transport-Security: max-age=31536000\r\nX-Content-Type-Options: nosniff\r\nX-XSS-Protection: 1; mode=block\r\nVary: Accept-Encoding\r\nX-Cache: Hit from cloudfront\r\nVia: 1.1 7ba3caf71ae7a52dd411d1a543e80cd8.cloudfront.net (CloudFront)\r\nX-Amz-Cf-Pop: SFO5-C3\r\nX-Amz-Cf-Id: w4h42tkoJD-rEpkRDZUvnQBmy26GVGe6pUsuRr1Dphf7oajYbjXaOA==\r\nAge: 132\r\n", "responseTime": 14, "roundId": 1588608900, "serverIp": "99.84.230.17", "sslCerts": [ { "daysUntilExpiry": 7, "fetchDateInValidCertDateRange": true, "issuerName": "DigiCert SHA2 Extended Validation Server CA", "notValidAfter": "2020-05-12 12:00:00", "notValidBefore": "2018-03-27 00:00:00", "subjectAltNames": [ "www.thousandeyes.com", "thousandeyes.com" ], "subjectName": "www.thousandeyes.com" }, { "daysUntilExpiry": 3092, "fetchDateInValidCertDateRange": true, "issuerName": "DigiCert High Assurance EV Root CA", "notValidAfter": "2028-10-22 12:00:00", "notValidBefore": "2013-10-22 12:00:00", "subjectName": "DigiCert SHA2 Extended Validation Server CA" }, { "daysUntilExpiry": 4206, "fetchDateInValidCertDateRange": true, "issuerName": "DigiCert High Assurance EV Root CA", "notValidAfter": "2031-11-10 00:00:00", "notValidBefore": "2006-11-10 00:00:00", "subjectName": "DigiCert High Assurance EV Root CA" } ], "sslCipher": "ECDHE-RSA-AES128-GCM-SHA256", "sslTime": 9, "sslVersion": "TLSv1.2", "totalTime": 15, "waitTime": 3, "wireSize": 9993 ], "test": { "alertsEnabled": 1, "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/tests/817", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/web/http-server/817", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/metrics/817", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/path-vis/817", "rel": "data" } ], "authType": "NONE", "bandwidthMeasurements": 0, "bgpMeasurements": 0, "contentRegex": "", "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "enabled": 1, "followRedirects": 1, "httpTargetTime": 1000, "httpTimeLimit": 5, "httpVersion": 2, "interval": 900, "ipv6Policy": "USE_AGENT_POLICY", "liveShare": 0, "modifiedBy": "ThousandEyes (support@thousandeyes.com)", "modifiedDate": "2019-01-17 12:38:09", "mtuMeasurements": 1, "networkMeasurements": 1, "numPathTraces": 3, "pathTraceMode": "classic", "probeMode": "AUTO", "protocol": "TCP", "savedEvent": 0, "sslVersion": "Auto", "sslVersionId": 0, "testId": 817, "testName": "http://www.thousandeyes.com", "type": "http-server", "url": "http://www.thousandeyes.com", "useNtlm": 0, "usePublicBgp": 1, "verifyCertificate": 1 } } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/page-load/{testId}` (Web) Page load](broken-reference)

Returns response time, total size, count of objects and errors, and provides page and DOM load times for a web page.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the page load test you for wish to retrieve data
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field        | Data Type | Units        | Notes                                                       |
| ------------ | --------- | ------------ | ----------------------------------------------------------- |
| agentId      | integer   | n/a          | unique ID of agent, from `/agents` endpoint                 |
| agentName    | string    | n/a          | display name of the agent responding                        |
| countryId    | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                |
| date         | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                 |
| roundId      | long      | seconds      | epoch time (seconds) indicating the start time of the round |
| permalink    | url       | n/a          | link to jump to this result in the front end                |
| responseTime | integer   | milliseconds | time to first byte                                          |
| totalSize    | integer   | bytes        | sum of wire size of all objects on page                     |
| numObjects   | integer   | n/a          | number of objects found on the page                         |
| numErrors    | integer   | n/a          | number of objects which encountered errors during download  |
| domLoadTime  | integer   | milliseconds | time to interaction                                         |
| pageLoadTime | integer   | milliseconds | time to completely load page                                |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/web/page-load/818.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 08 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493288220 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "web": { "test": { "createdDate": "2012-06-28 19:34:33", "modifiedDate": "2016-09-20 23:01:55", "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 818, "testName": "http://www.google.com", "type": "page-load", "interval": 900, "httpInterval": 900, "url": "http://www.google.com", "protocol": "TCP", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "usePublicBgp": 1, "alertsEnabled": 0, "liveShare": 0, "httpTimeLimit": 5, "httpTargetTime": 1000, "httpVersion": 2, "pageLoadTimeLimit": 30, "pageLoadTargetTime": 2, "followRedirects": 1, "includeHeaders": 0, "sslVersionId": 0, "sslVersion": "Auto" "verifyCertificate": 1, "useNtlm": 0, "authType": "NONE", "contentRegex": "", "probeMode": "AUTO", "pathTraceMode": "classic", "apiLinks": [...] }, "pageLoad": [ { "agentName": "Kwai Chung, Hong Kong", "countryId": "HK", "date": "2018-07-12 14:00:24", "agentId": 12, "roundId": 1531404000, "responseTime": 34, "totalSize": 403301, "numObjects": 17, "numErrors": 0, "domLoadTime": 352, "pageLoadTime": 352, "permalink": "https://app.thousandeyes.com/web/page-load?__a=75&testId=818&roundId=1531404000&agentId=12" }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/page-load/{testId}/{agentId}/{roundId}` (Web) Page load component detail](broken-reference)

Returns HAR (http archive) information, including component list and timing for elements loaded in a Page Load test. This is analogous to what is shown in the waterfall view for a Page Load test, with an agent selected. Includes response data, dns, connect, ssl, send, wait and receive times for each component loaded in a page.

Note: this endpoint is only available in v5 or higher of the ThousandEyes API

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the Page Load test you for wish to retrieve data
* `{agentId}` the ID of the agent for which you wish to retrieve data
* `{roundId}` the ID of the round for which you wish to retrieve data
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Response data is returned according to the [HAR specification](http://www.softwareishard.com/blog/har-12-spec/).

| Field        | Data Type | Units        | Notes                                                                                 |
| ------------ | --------- | ------------ | ------------------------------------------------------------------------------------- |
| agentId      | integer   | n/a          | unique ID of agent, from `/agents` endpoint                                           |
| agentName    | string    | n/a          | display name of the agent responding                                                  |
| countryId    | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                                          |
| date         | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                                           |
| roundId      | long      | seconds      | epoch time (seconds) indicating the start time of the round                           |
| permalink    | url       | n/a          | link to jump to this result in the front end                                          |
| responseTime | integer   | milliseconds | time to first byte                                                                    |
| totalSize    | integer   | bytes        | sum of wire size of all objects on page                                               |
| numObjects   | integer   | n/a          | number of objects found on the page                                                   |
| numErrors    | integer   | n/a          | number of objects which encountered errors during download                            |
| domLoadTime  | integer   | milliseconds | time to interaction                                                                   |
| pageLoadTime | integer   | milliseconds | time to completely load page                                                          |
| har          | har\*     | n/a          | see [HAR specification](http://www.softwareishard.com/blog/har-12-spec/) for details. |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/web/page-load/818/12/1493288100.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 08 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493288220 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "web": { "test": { "createdDate": "2012-06-28 19:34:33", "modifiedDate": "2016-09-20 23:01:55", "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 818, "testName": "http://www.google.com", "type": "page-load", "interval": 900, "httpInterval": 900, "url": "http://www.google.com", "protocol": "TCP", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "usePublicBgp": 1, "alertsEnabled": 0, "liveShare": 0, "httpTimeLimit": 5, "httpTargetTime": 1000, "httpVersion": 2, "pageLoadTimeLimit": 30, "pageLoadTargetTime": 2, "followRedirects": 1, "includeHeaders": 0, "sslVersionId": 0, "sslVersion": "Auto", "verifyCertificate": 1, "useNtlm": 0, "authType": "NONE", "contentRegex": "", "probeMode": "AUTO", "pathTraceMode": "classic", "apiLinks": [...] }, "pageLoad": [ { "har": { "log": { "creator": { "name": "ThousandEyes DB Exporter" }, "entries": [ { "pageref": "page_0", "serverIPAddress": "2404:6800:4005:80d::2004", "startedDateTime": "2018-07-12T16:00:26.948Z", "time": 37, "timings": { "blocked": 7, "dns": -1, "connect": -1, "ssl": -1, "send": 0, "wait": 28, "receive": 2 }, "request": { "url": "http://www.google.com/", "headers": [ { "name": "Accept", "value": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8" }, ... ], "method": "GET" }, "response": { "headersSize": 649, "bodySize": 231, "status": 302, "headers": [ { "name": "Cache-Control", "value": "private" }, ... ], "content": { "size": 231, "mimeType": "text/html" }, "redirectURL": "", "statusText": "FOUND" "statusText": "FOUND" } }, ... "pages": [ { "id": "page_0", "title": "Google", "startedDateTime": "2018-07-12T16:00:26.946Z", "responseCode": 0, "pageTimings": { "onLoad": 504, "onContentLoad": 344 } } ], "version": "1.2" } }, "agentName": "Kwai Chung, Hong Kong", "countryId": "HK", "date": "2018-07-12 16:00:31", "agentId": 12, "roundId": 1531411200, "responseTime": 35, "totalSize": 404397, "numObjects": 19, "numErrors": 0, "domLoadTime": 344, "pageLoadTime": 504, "permalink": "https://app.thousandeyes.com/web/page-load?__a=null&testId=818&roundId=1531411200&agentId=12" } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/web-transactions/{testId}` (Web) Web Transactions](broken-reference)

Returns test configuration, and transaction time and errors from each agent selected to run a web transaction. A **time frame** must be specified, or the current round of data will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the web transaction you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field           | Data Type | Units        | Notes                                                       |
| --------------- | --------- | ------------ | ----------------------------------------------------------- |
| agentId         | integer   | n/a          | unique ID of agent, from `/agents` endpoint                 |
| agentName       | string    | n/a          | display name of the agent responding                        |
| countryId       | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                |
| date            | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                 |
| roundId         | long      | seconds      | epoch time (seconds) indicating the start time of the round |
| permalink       | url       | n/a          | link to jump to this result in the front end                |
| componentErrors | integer   | n/a          | number of components which did not successfully load        |
| transactionTime | integer   | milliseconds | elapsed execution time of the web transaction script        |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/web/web-transactions/1161561.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Fri, 15 Nov 2019 16:36:19 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: f72ql Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1573835820 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "pages": { "current": 1 }, "web": { "test": { "alertsEnabled": 0, "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/tests/1161561", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/net/metrics/1161561", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/path-vis/1161561", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/bgp-metrics/1161561", "rel": "data" } ], "authType": "NONE", "bandwidthMeasurements": 0, "bgpMeasurements": 1, "contentRegex": "", "createdBy": "ThousandEyes (support@thousandeyes.com)", "createdDate": "2019-11-15 16:29:55", "credentials": [], "enabled": 1, "followRedirects": 1, "httpTargetTime": 1000, "httpTimeLimit": 5, "httpVersion": 2, "includeHeaders": 1, "interval": 600, "liveShare": 0, "modifiedBy": "ThousandEyes (support@thousandeyes.com)", "modifiedDate": "2019-11-15 16:31:11", "mtuMeasurements": 1, "networkMeasurements": 1, "numPathTraces": 3, "probeMode": "AUTO", "pathTraceMode": "classic", "protocol": "TCP", "savedEvent": 0, "sslVersion": "Auto", "sslVersionId": 0, "targetTime": 10, "testId": 1161561, "testName": "Google.com Web Transaction", "timeLimit": 30, "transactionScript": "import { By, Key, until } from 'selenium-webdriver';\nimport { driver, markers, credentials, downloads, transaction } from 'thousandeyes';\n\nrunScript();\n\nasync function runScript() {\n\n // Load page\n await driver.get('https://google.com');\n await driver.takeScreenshot();\n \n // Search\n markers.start('SearchForWebdriver');\n await driver.findElement(By.name('q')).sendKeys('webdriver', Key.RETURN);\n await driver.takeScreenshot();\n markers.stop('SearchForWebdriver');\n\n // Wait for full page load\n await driver.wait(until.titleIs('webdriver - Google Search'), 1000);\n await driver.takeScreenshot();\n};\n ", "type": "web-transactions", "url": "https://google.com", "useNtlm": 0, "usePublicBgp": 1, "verifyCertificate": 1 }, "webTransaction": [ { "agentId": 31, "agentName": "Chicago, IL", "componentErrors": 5, "countryId": "US", "date": "2019-11-15 16:32:44", "permalink": "https://app.thousandeyes.com/null?__a=75&testId=1161561&roundId=1573835400&agentId=31", "roundId": 1573835400, "transactionTime": 2379 }, { "agentId": 10, "agentName": "Paris, France", "componentErrors": 5, "countryId": "FR", "date": "2019-11-15 16:32:55", "errorDetails": "TimeoutError: Waiting for title to be \"webdriver - Google Search\"\nWait timed out after 1002ms", "errorType": "OTHER", "permalink": "https://app.thousandeyes.com/null?__a=75&testId=1161561&roundId=1573835400&agentId=10", "roundId": 1573835400 } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/web-transactions/{testId}/{agentId}/{roundId}` (Web) Web Transaction detail](broken-reference)

Returns transaction time, marker duration, error counts, and pages transited during the execution of a web transaction. An `agentId` and `roundId` is required, since results from a single round of a web transaction execution will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the web transaction you wish to retrieve
* `{agentId}` the ID of the agent for which you wish to obtain transaction data
* `{roundId}` the roundID for which data is being requested
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field                | Data Type | Units        | Notes                                                                 |
| -------------------- | --------- | ------------ | --------------------------------------------------------------------- |
| agentId              | integer   | n/a          | unique ID of agent, from `/agents` endpoint                           |
| agentName            | string    | n/a          | display name of the agent responding                                  |
| countryId            | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                          |
| date                 | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                           |
| roundId              | long      | seconds      | epoch time (seconds) indicating the start time of the round           |
| permalink            | url       | n/a          | link to jump to this result in the front end                          |
| transactionTime      | integer   | milliseconds | elapsed execution time of the web transaction script                  |
| componentErrors      | integer   | n/a          | total number of component errors encountered during load of this page |
| markers              | array     | n/a          | see below                                                             |
| markers.name         | string    | n/a          | name assigned to marker in transaction script                         |
| markers.duration     | integer   | milliseconds | total time recorded by marker                                         |
| pages                | array     | n/a          | see below                                                             |
| pages.pageNum        | integer   | n/a          | page index                                                            |
| pages.pageName       | string    | n/a          | meta title value for page visited                                     |
| pages.componentCount | integer   | n/a          | number of components on target page                                   |
| pages.errorCount     | integer   | n/a          | number of errors encountered during page load                         |
| pages.duration       | integer   | milliseconds | time spent on page                                                    |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/web/web-transactions/1161561/31/1573836000.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Fri, 15 Nov 2019 16:59:49 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: fjxcv Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 232 X-Organization-Rate-Limit-Reset: 1573837200 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "web": { "test": { "createdDate": "2019-11-15 16:29:55", "modifiedDate": "2019-11-15 16:31:11", "createdBy": "ThousandEyes (support@thousandeyes.com)", "modifiedBy": "ThousandEyes (support@thousandeyes.com)", "enabled": 1, "savedEvent": 0, "testId": 1161561, "testName": "Google.com Web Transaction", "type": "web-transactions", "interval": 600, "url": "https://google.com", "protocol": "TCP", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "usePublicBgp": 1, "alertsEnabled": 0, "liveShare": 0, "timeLimit": 30, "targetTime": 10, "httpTimeLimit": 5, "httpTargetTime": 1000, "httpVersion": 2, "followRedirects": 1, "includeHeaders": 1, "sslVersionId": 0, "verifyCertificate": 1, "useNtlm": 0, "authType": "NONE", "contentRegex": "", "transactionScript": "import { By, Key, until } from 'selenium-webdriver';\nimport { driver, markers, credentials, downloads, transaction } from 'thousandeyes';\n\nrunScript();\n\nasync function runScript() {\n\n // Load page\n await driver.get('https://google.com');\n await driver.takeScreenshot();\n \n // Search\n markers.start('SearchForWebdriver');\n await driver.findElement(By.name('q')).sendKeys('webdriver', Key.RETURN);\n await driver.takeScreenshot();\n markers.stop('SearchForWebdriver');\n\n // Wait for full page load\n await driver.wait(until.titleIs('webdriver - Google Search'), 1000);\n await driver.takeScreenshot();\n};\n ", "probeMode": "AUTO", "pathTraceMode": "classic", "numPathTraces": 3, "credentials": [], "apiLinks": [ { "rel": "self", "href": "https://api.thousandeyes.com/v6/tests/1161561" }, { "rel": "data", "href": "https://api.thousandeyes.com/v6/net/metrics/1161561" }, { "rel": "data", "href": "https://api.thousandeyes.com/v6/net/path-vis/1161561" }, { "rel": "data", "href": "https://api.thousandeyes.com/v6/net/bgp-metrics/1161561" } ], "sslVersion": "Auto" }, "webTransaction": [ { "agentName": "Chicago, IL", "countryId": "US", "date": "2019-11-15 16:42:00", "permalink": "https://app.thousandeyes.com/null?__a=75&testId=1161561&roundId=1573836000&agentId=31", "roundId": 1573836000, "agentId": 31, "componentErrors": 6, "markers": [ { "name": "SearchForWebdriver", "duration": 1360.0 } ], "pages": [ { "pageNum": 0, "pageName": "Google", "duration": 1117.5660001039505 }, { "pageNum": 1, "pageName": "webdriver - Google Search", "duration": 1146.6330000162125 } ], "transactionTime": 2341 } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/web-transactions/{testId}/{agentId}/{roundId}/{pageNum}` (Web) Web Transaction component detail](broken-reference)

Returns HAR (http archive) information, including component list and timing for elements loaded in a web transaction test. This is analogous to what is shown in the waterfall view for a page load or transaction test, with an agent selected. Includes response data, dns, connect, ssl, send, wait and receive times for each component loaded in a page.

Note: this endpoint is only available in v5 or higher of the ThousandEyes API.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the Web Transaction test you for wish to retrieve data
* `{agentId}` the ID of the agent for which you wish to retrieve data
* `{roundId}` the ID of the round for which you wish to retrieve data
* `{pageNum}` the page number for the page reached in a transaction. Can be obtained from `/web/web-transactions/{testId}/{agentId}/{roundId}` endpoint. Page numbers are zero-indexed.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Response data is returned according to the [HAR specification](http://www.softwareishard.com/blog/har-12-spec/).

| Field                | Data Type | Units        | Notes                                                                                 |
| -------------------- | --------- | ------------ | ------------------------------------------------------------------------------------- |
| agentId              | integer   | n/a          | unique ID of agent, from `/agents` endpoint                                           |
| agentName            | string    | n/a          | display name of the agent responding                                                  |
| countryId            | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                                          |
| date                 | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                                           |
| roundId              | long      | seconds      | epoch time (seconds) indicating the start time of the round                           |
| permalink            | url       | n/a          | link to jump to this result in the front end                                          |
| markers              | array     | n/a          | see below                                                                             |
| markers.name         | string    | n/a          | name assigned to marker in transaction script                                         |
| markers.duration     | integer   | milliseconds | total time recorded by marker                                                         |
| pages                | array     | n/a          | see below                                                                             |
| pages.pageNum        | integer   | n/a          | page index                                                                            |
| pages.pageName       | string    | n/a          | meta title value for page visited                                                     |
| pages.componentCount | integer   | n/a          | number of components on target page                                                   |
| pages.errorCount     | integer   | n/a          | number of errors encountered during page load                                         |
| pages.duration       | integer   | milliseconds | time spent on page                                                                    |
| transactionTime      | integer   | milliseconds | elapsed execution time of the web transaction script                                  |
| har                  | har\*     | n/a          | see [HAR specification](http://www.softwareishard.com/blog/har-12-spec/) for details. |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/web/web-transactions/1161561/31/1573836000/0.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Fri, 15 Nov 2019 17:13:46 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: 8xb13 Cache-Control: no-store X-Organization-Rate-Limit-Limit: 1000 X-Organization-Rate-Limit-Remaining: 999 X-Organization-Rate-Limit-Reset: 1573838040 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "web": { "test": { "alertsEnabled": 0, "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/tests/1161561", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/net/metrics/1161561", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/path-vis/1161561", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/bgp-metrics/1161561", "rel": "data" } ], "authType": "NONE", "bandwidthMeasurements": 0, "bgpMeasurements": 1, "contentRegex": "", "createdBy": "ThousandEyes (support@thousandeyes.com)", "createdDate": "2019-11-15 16:29:55", "credentials": [], "enabled": 1, "followRedirects": 1, "httpTargetTime": 1000, "httpTimeLimit": 5, "httpVersion": 2, "includeHeaders": 1, "interval": 600, "liveShare": 0, "modifiedBy": "ThousandEyes (support@thousandeyes.com)", "modifiedDate": "2019-11-15 16:31:11", "mtuMeasurements": 1, "networkMeasurements": 1, "numPathTraces": 3, "probeMode": "AUTO", "pathTraceMode": "classic", "protocol": "TCP", "savedEvent": 0, "sslVersion": "Auto", "sslVersionId": 0, "targetTime": 10, "testId": 1161561, "testName": "Google.com Web Transaction", "timeLimit": 30, "transactionScript": "import { By, Key, until } from 'selenium-webdriver';\nimport { driver, markers, credentials, downloads, transaction } from 'thousandeyes';\n\nrunScript();\n\nasync function runScript() {\n\n // Load page\n await driver.get('https://google.com');\n await driver.takeScreenshot();\n \n // Search\n markers.start('SearchForWebdriver');\n await driver.findElement(By.name('q')).sendKeys('webdriver', Key.RETURN);\n await driver.takeScreenshot();\n markers.stop('SearchForWebdriver');\n\n // Wait for full page load\n await driver.wait(until.titleIs('webdriver - Google Search'), 1000);\n await driver.takeScreenshot();\n};\n ", "type": "web-transactions", "url": "https://google.com", "useNtlm": 0, "usePublicBgp": 1, "verifyCertificate": 1 }, "webTransaction": [ { "agentId": 31, "agentName": "Chicago, IL", "componentErrors": 6, "countryId": "US", "date": "2019-11-15 16:42:00", "har": { "log": { "creator": { "name": "ThousandEyes DB Exporter" }, "entries": [ { "pageref": "page_0", "request": { "headers": [ { "name": ":authority", "value": "google.com" }, { "name": ":method", "value": "GET" }, { "name": ":path", "value": "/" }, { "name": ":scheme", "value": "https" }, { "name": "accept", "value": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8" }, { "name": "accept-encoding", "value": "gzip, deflate, br" }, { "name": "accept-language", "value": "en-US,en;q=0.9" }, { "name": "upgrade-insecure-requests", "value": "1" }, { "name": "user-agent", "value": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.83 Safari/537.36" }, { "name": "x-thousandeyes-agent", "value": "yes" } ], "method": "GET", "url": "https://google.com/" }, "response": { "bodySize": 220, "content": { "mimeType": "text/html", "size": 220 }, "headers": [ { "name": "alt-svc", "value": "quic=\":443\"; ma=2592000; v=\"46,43\",h3-Q050=\":443\"; ma=2592000,h3-Q049=\":443\"; ma=2592000,h3-Q048=\":443\"; ma=2592000,h3-Q046=\":443\"; ma=2592000,h3-Q043=\":443\"; ma=2592000" }, { "name": "cache-control", "value": "public, max-age=2592000" }, { "name": "content-length", "value": "220" }, { "name": "content-type", "value": "text/html; charset=UTF-8" }, { "name": "date", "value": "Fri, 15 Nov 2019 16:41:54 GMT" }, { "name": "expires", "value": "Sun, 15 Dec 2019 16:41:54 GMT" }, { "name": "location", "value": "https://www.google.com/" }, { "name": "server", "value": "gws" }, { "name": "status", "value": "301" }, { "name": "x-frame-options", "value": "SAMEORIGIN" }, { "name": "x-xss-protection", "value": "0" } ], "headersSize": 471, "redirectURL": "", "status": 301, "statusText": "MOVED_PERMANENTLY" }, "serverIPAddress": "172.217.6.110", "startedDateTime": "2019-11-15T16:41:54.798Z", "time": 71, "timings": { "blocked": 2, "connect": 16, "dns": 1, "receive": 1, "send": 0, "ssl": 14, "wait": 50 } }, { "pageref": "page_0", "request": { "headers": [ { "name": ":authority", "value": "www.google.com" }, { "name": ":method", "value": "GET" }, { "name": ":path", "value": "/" }, { "name": ":scheme", "value": "https" }, { "name": "accept", "value": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8" }, { "name": "accept-encoding", "value": "gzip, deflate, br" }, { "name": "accept-language", "value": "en-US,en;q=0.9" }, { "name": "upgrade-insecure-requests", "value": "1" }, { "name": "user-agent", "value": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.83 Safari/537.36" }, { "name": "x-thousandeyes-agent", "value": "yes" } ], "method": "GET", "url": "https://www.google.com/" }, "response": { "bodySize": 65214, "content": { "mimeType": "text/html", "size": 225039 }, "headers": [ { "name": "alt-svc", "value": "quic=\":443\"; ma=2592000; v=\"46,43\",h3-Q050=\":443\"; ma=2592000,h3-Q049=\":443\"; ma=2592000,h3-Q048=\":443\"; ma=2592000,h3-Q046=\":443\"; ma=2592000,h3-Q043=\":443\"; ma=2592000" }, { "name": "cache-control", "value": "private, max-age=0" }, { "name": "content-encoding", "value": "br" }, { "name": "content-length", "value": "65214" }, { "name": "content-type", "value": "text/html; charset=UTF-8" }, { "name": "date", "value": "Fri, 15 Nov 2019 16:41:54 GMT" }, { "name": "expires", "value": "-1" }, { "name": "p3p", "value": "CP=\"This is not a P3P policy! See g.co/p3phelp for more info.\"" }, { "name": "server", "value": "gws" }, { "name": "set-cookie", "value": "(removed)" }, { "name": "status", "value": "200" }, { "name": "strict-transport-security", "value": "max-age=31536000" }, { "name": "x-frame-options", "value": "SAMEORIGIN" }, { "name": "x-xss-protection", "value": "0" } ], "headersSize": 915, "redirectURL": "", "status": 200, "statusText": "OK" }, "serverIPAddress": "172.217.4.196", "startedDateTime": "2019-11-15T16:41:54.870Z", "time": 182, "timings": { "blocked": 2, "connect": 4, "dns": 0, "receive": 58, "send": 0, "ssl": 2, "wait": 118 } }, ... ], "pages": [ { "id": "page_0", "pageTimings": { "onContentLoad": 367, "onLoad": 737 }, "responseCode": 0, "startedDateTime": "2019-11-15T16:41:54.796Z", "title": "Google" } ], "version": "1.2" } }, "markers": [ { "duration": 1360.0, "name": "SearchForWebdriver" } ], "pages": [ { "duration": 1117.5660001039505, "pageName": "Google", "pageNum": 0 }, { "duration": 1146.6330000162125, "pageName": "webdriver - Google Search", "pageNum": 1 } ], "permalink": "https://app.thousandeyes.com/null?__a=75&testId=1161561&roundId=1573836000&agentId=31", "roundId": 1573836000, "transactionTime": 2341 } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/web/ftp-server/{testId}` (Web) FTP server](broken-reference)

Returns response code, response and fetch times, as well as component-level (DNS, Connect, Negotiation, Response and Transfer) timing for the load of an object over FTP. FTP tests support plain text FTP, FTPS (FTP over SSL), and SFTP (secure FTP).

_Note_: this endpoint is only available in API v6 and higher.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the HTTP Server (or page load) test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field           | Data Type | Units        | Notes                                                                      |
| --------------- | --------- | ------------ | -------------------------------------------------------------------------- |
| agentId         | integer   | n/a          | unique ID of agent, from `/agents` endpoint                                |
| agentName       | string    | n/a          | display name of the agent responding                                       |
| countryId       | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                               |
| date            | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                                |
| roundId         | long      | seconds      | epoch time (seconds) indicating the start time of the round                |
| permalink       | url       | n/a          | link to jump to this result in the front end                               |
| serverIp        | string    | n/a          | IP address of destination server                                           |
| responseCode    | integer   | n/a          | code of FTP response                                                       |
| dnsTime         | float     | milliseconds | time required to resolve DNS                                               |
| connectTime     | fload     | milliseconds | time required to establish a TCP connection to the server                  |
| negotiationTime | float     | milliseconds | time negotiate the connection and authenticate with the destination server |
| waitTime        | float     | milliseconds | time elapsed between completion of request and first byte of response      |
| responseTime    | float     | milliseconds | sum of DNS, connect, negotiation and wait times                            |
| transferTime    | float     | milliseconds | elapsed time between first and last byte of the transfer                   |
| wireSize        | float     | bytes        | size of content, in bytes                                                  |
| totalTime       | integer   | milliseconds | sum of response + transfer time                                            |
| errorType       | string    | n/a          | type of error encountered; corresponds to phase of connection              |
| errorDetails    | string    | n/a          | error details, if an error were encountered                                |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/web/ftp-server/367580.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 08 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1493288220 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "pages": { "current": 1 }, "web": { "ftpServer": [ { "agentId": 144, "agentName": "Vienna, Austria", "connectTime": 50.153, "countryId": "AT", "date": "2017-04-27 11:44:13", "dnsTime": 0.589, "errorType": "None", "negotiationTime": 503.413, "permalink": "https://app.thousandeyes.com/web/ftp-server?__a=75&testId=367580&roundId=1493293440&agentId=144", "responseCode": 226, "responseTime": 605.689, "roundId": 1493293440, "serverIp": "193.2.1.88", "throughput": 222019, "totalTime": 705.554, "transferTime": 99.865, "waitTime": 52.1, "wireSize": 22172 } ], "test": { "alertsEnabled": 0, "apiLinks": [...], "bandwidthMeasurements": 0, "bgpMeasurements": 1, "createdBy": "Deleted User", "createdDate": "2017-04-27 11:40:12", "enabled": 1, "ftpTargetTime": 1000, "ftpTimeLimit": 10, "interval": 120, "liveShare": 0, "modifiedBy": "Deleted User", "modifiedDate": "2017-04-27 11:42:31", "mtuMeasurements": 1, "networkMeasurements": 1, "requestType": "List", "savedEvent": 0, "testId": 367580, "testName": "ftp://ftp.arnes.si", "type": "ftp-server", "url": "ftp://ftp.arnes.si/packages/gnu/", "useActiveFtp": 0, "useExplicitFtps": 0, "username": "anonymous" } } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dns/trace/{testId}` (DNS) Domain trace](broken-reference)

Returns a DNS record from the vantage point of the agent. Similar to `dig +trace`.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the DNS trace test you wish to retrieve.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Take note of the output field in the response body below – depending on the record type requested, the data can be extremely verbose. Test metadata is shown in the first element of the response (test), and the “trace” element follows as the second element, showing an array of responses (one from each agent).

| Field              | Data Type | Units        | Notes                                                         |
| ------------------ | --------- | ------------ | ------------------------------------------------------------- |
| agentId            | integer   | n/a          | unique ID of agent, from `/agents` endpoint                   |
| agentName          | string    | n/a          | display name of the agent responding                          |
| countryId          | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                  |
| date               | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                   |
| roundId            | long      | seconds      | epoch time (seconds) indicating the start time of the round   |
| permalink          | url       | n/a          | link to jump to this result in the front end                  |
| output             | string    | n/a          | verbose output from the trace request                         |
| errorDetails       | string    | n/a          | if an error was encountered, error text                       |
| queries            | integer   | n/a          | how many queries were required to get to the requested result |
| failedQueries      | integer   | n/a          | how many queries failed while getting to the requested result |
| finalServerQueried | string    | n/a          | DNS server that provided the final result                     |
| finalQueryTime     | integer   | milliseconds | how long the final query took to return a response            |
| mappings           | string    | n/a          | final mappings returned from the request                      |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dns/trace/820.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Sat, 08 Feb 2020 16:55:04 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: d7nds Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1581180960 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "dns": { "test": { "enabled": 1, "testId": 17594, "testName": "thousandeyes.com A", "type": "dns-trace", "interval": 900, "domain": "thousandeyes.com A", "modifiedDate": "2014-01-21 03:19:16", "createdBy": "API Sandbox Admin (api.sandbox+admin@thousandeyes.com)", "modifiedBy": "API Sandbox Admin (api.sandbox+admin@thousandeyes.com)", "createdDate": "2014-01-21 03:19:16", "savedEvent": 0, "liveShare": 0, "dnsTransportProtocol": "UDP", "dnsQueryClass": "IN", "alertsEnabled": 1, "apiLinks": [...] }, "trace": [ { "agentName": "São Paulo, Brazil", "countryId": "BR", "date": "2014-01-21 03:20:09", "output": "com.\t172800\tIN\tNS\ta.gtld-servers.net.\ncom.\t172800\tIN\tNS\tf.gtld-servers.net.\ncom.\t172800\tIN\tNS\tc.gtld-servers.net.\ncom.\t172800\tIN\tNS\tb.gtld-servers.net.\ncom.\t172800\tIN\tNS\td.gtld-servers.net.\ncom.\t172800\tIN\tNS\te.gtld-servers.net.\ncom.\t172800\tIN\tNS\tg.gtld-servers.net.\ncom.\t172800\tIN\tNS\tm.gtld-servers.net.\ncom.\t172800\tIN\tNS\th.gtld-servers.net.\ncom.\t172800\tIN\tNS\tj.gtld-servers.net.\ncom.\t172800\tIN\tNS\ti.gtld-servers.net.\ncom.\t172800\tIN\tNS\tl.gtld-servers.net.\ncom.\t172800\tIN\tNS\tk.gtld-servers.net.\n;; Received 498 bytes from 199.7.91.13(d.root-servers.net.) in 119 ms\n\nthousandeyes.com.\t172800\tIN\tNS\ta1.verisigndns.com.\nthousandeyes.com.\t172800\tIN\tNS\ta2.verisigndns.com.\nthousandeyes.com.\t172800\tIN\tNS\ta3.verisigndns.com.\nthousandeyes.com.\t172800\tIN\tNS\tu1.verisigndns.com.\n;; Received 266 bytes from 192.5.6.30(a.gtld-servers.net.) in 178 ms\n\napp.thousandeyes.com.\t300\tIN\tCNAME\tweb.thousandeyes.com.\nweb.thousandeyes.com.\t300\tIN\tCNAME\tlb-app.thousandeyes.com.\nlb-app.thousandeyes.com.\t3600\tIN\tA\t208.185.7.120\n;; Received 173 bytes from 209.112.113.33(a1.verisigndns.com.) in 178 ms\n\n", "permalink": "https://app.thousandeyes.com/dns/trace?__a=75&testId=17594&roundId=1390274400&agentId=16", "agentId": 16, "errorDetails": "", "queries": 3, "failedQueries": 0, "finalServerQueried": "a1.verisigndns.com.", "finalQueryTime": 178, "mappings": "208.185.7.120" }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dns/server/{testId}/{serverId}` (DNS) Server metrics](broken-reference)

Returns the mappings for a DNS record, along with resolution time to each authoritative server, as measured from the vantage point of the agent. Similar to `dig @server`.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the DNS server test you wish to retrieve.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

The DNS Server tests are somewhat unique, in that you are testing multiple targets with a single test configuration. For example - if you’re testing com. NS, you’ll actually end up with 13 tests, since the test should be targeting 13 different nameservers \[a-m].gtld-servers.net. This test tests resolution time to each of the authoritative nameservers from each agent, ending up with something of a matrix of test results for each iteration.

For tests with Network Measurements enabled (`"networkMeasurements": 1`), you’ll need the serverId identified in the test to pull network metrics for your DNS server test. Syntax for DNS Server network metrics [see End-to-End Metrics](broken-reference) is as follows:

`$ curl https://api.thousandeyes.com/v6/dns/server/{testId}/{serverId}.json \ -u {email}:{authToken}`

| Field          | Data Type | Units        | Notes                                                         |
| -------------- | --------- | ------------ | ------------------------------------------------------------- |
| agentId        | integer   | n/a          | unique ID of agent, from `/agents` endpoint                   |
| agentName      | string    | n/a          | display name of the agent responding                          |
| countryId      | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                  |
| date           | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                   |
| roundId        | long      | seconds      | epoch time (seconds) indicating the start time of the round   |
| permalink      | url       | n/a          | link to jump to this result in the front end                  |
| serverId       | integer   | n/a          | internal ID of DNS server being tested                        |
| server         | string    | n/a          | canonical name of server being tested                         |
| resolutionTime | integer   | milliseconds | how long it took to run the query against the server          |
| errorDetails   | string    | n/a          | if an error was encountered, error text                       |
| queries        | integer   | n/a          | how many queries were reuqired to get to the requested result |
| mappings       | string    | n/a          | final mappings returned from the request                      |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dns/server/821.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Sat, 08 Feb 2020 16:55:04 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: d7nds Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1581180960 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "dns": { "test": { "enabled": 1, "testId": 821, "testName": "thousandeyes.com ANY", "type": "dns-server", "interval": 900, "domain": "thousandeyes.com ANY", "dnsServers": [ { "serverId": 465, "serverName": "a1.verisigndns.com." } ], "modifiedDate": "2013-05-11 02:02:16", "networkMeasurements": 1, "mtuMeasurements": 1, "bandwidthMeasurements": 0, "bgpMeasurements": 1, "usePublicBgp": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 20:47:29", "dnsQueryClass": "IN", "dnsTransportProtocol": "UDP", "ipv6Policy": "USE_AGENT_POLICY", "apiLinks": [...] }, "server": [ { "agentName": "Hong Kong", "countryId": "HK", "date": "2013-11-13 04:30:20", "permalink": "https://app.thousandeyes.com/dns/server?__a=75&testId=821&roundId=1384317000&serverId=465&agentId=12", "agentId": 12, "serverId": 465, "server": "a1.verisigndns.com.", "resolutionTime": 3, "roundId": 1384317000, "errorDetails": "", "mappings": "a1.verisigndns.com. dnssupport.verisign-grs.com. 2284831191 28800 7200 1209600 3600 (SOA)\na1.verisigndns.com. (NS)\nu1.verisigndns.com. (NS)\na2.verisigndns.com. (NS)\na3.verisigndns.com. (NS)\n54.215.17.122 (A)\n0 aspmx.l.google.com. (MX)\n5 alt1.aspmx.l.google.com. (MX)\n10 aspmx3.googlemail.com. (MX)\n5 alt2.aspmx.l.google.com. (MX)\n10 aspmx2.googlemail.com. (MX)\n\"7LO6JGX\" (TXT)\n\"v=spf1 ip4:65.122.4.140 ip4:208.185.7.125 include:_spf.google.com include:daredevil.thousandeyes.com include:sendgrid.net include:spf.braintreegateway.com include:emailer.hubspot.com include:eventbrite.com include:support.zendesk.com include:smtp.zendesk.\" \"com include:mktoma\\\" \\\"il.com ~all\" (TXT)\n\"google-site-verification=J9DoQXN_dDvzrDb53j_fETYTJjIRKOn-42sPbrJvpHA\" (TXT)" }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dns/dnssec/{testId}` (DNS) DNSSEC](broken-reference)

Returns the keychain validity for a record on a domain secured using DNSSEC extensions.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the DNSSEC test you wish to retrieve.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Validity can be measured using the errorDetails element, which will be populated in the event of an error validating the keychain.

| Field        | Data Type | Units   | Notes                                                       |
| ------------ | --------- | ------- | ----------------------------------------------------------- |
| agentName    | string    | n/a     | display name of the agent responding                        |
| countryId    | string    | n/a     | ISO-3166-1 alpha-2 country code of the agent                |
| date         | dateTime  | n/a     | yyyy-MM-dd hh:mm:ss, in UTC                                 |
| agentId      | integer   | n/a     | unique ID of agent, from `/agents` endpoint                 |
| roundId      | long      | seconds | epoch time (seconds) indicating the start time of the round |
| valid        | boolean   | n/a     | 1 for valid, 0 for invalid (see errorDetails field)         |
| permalink    | url       | n/a     | link to jump to this result in the front end                |
| errorDetails | string    | n/a     | if an error was encountered, error text                     |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dns/dnssec/822.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Thu, 08 Nov 2013 07:32:48 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1493294160 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dns": { "test": { "enabled": 1, "testId": 822, "testName": "thousandeyes.com A", "type": "dns-dnssec", "interval": 900, "domain": "thousandeyes.com A", "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 20:48:01", "apiLinks": [...] }, "dnssec": [ { "agentName": "Hong Kong", "countryId": "HK", "date": "2013-11-13 04:30:01", "valid": 0, "roundId": 1384317000, "permalink": "https://app.thousandeyes.com/dns/dnssec?__a=75&testId=822&roundId=1384317000&agentId=12", "agentId": 12, "errorDetails": "No DNSSEC public key(s) for thousandeyes.com A" }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/voice/sip-server/{testId}` (Voice) SIP server](broken-reference)

Returns voice SIP server metrics (response, invite, register time) from each agent, for each _roundId_ in the requested window. A **time frame** must be specified, or the current round of data will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` (Optional) specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` (Optional) specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` (Optional) specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` (Required) the ID of the SIP Server test for which you wish to retrieve data
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field           | Data Type | Units        | Notes                                                                                                          |
| --------------- | --------- | ------------ | -------------------------------------------------------------------------------------------------------------- |
| agentId         | integer   | n/a          | source agent unique Id, from `/agents` endpoint                                                                |
| agentName       | string    | n/a          | display name of the source agent                                                                               |
| authUser        | string    | n/a          | username used for authentication with SIP server (for `SIP Server` tests only)                                 |
| serverIp        | string    | n/a          | target agent IP address                                                                                        |
| countryId       | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                                                                   |
| date            | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                                                                    |
| roundId         | long      | seconds      | epoch time (seconds) indicating the start time of the round                                                    |
| permalink       | url       | n/a          | link to jump to this result in the front end                                                                   |
| availability    | float     | %            | availability of the service                                                                                    |
| connectTime     | integer   | milliseconds | time required to establish a TCP connection to the server, only available when TCP is configured as `protocol` |
| dnsTime         | integer   | milliseconds | time required to resolve DNS                                                                                   |
| inviteTime      | integer   | milliseconds | time to complete INVITE                                                                                        |
| numRedirects    | integer   | n/a          | number of redirects                                                                                            |
| optionsRequest  | string    | n/a          | entire OPTIONS request                                                                                         |
| optionsResponse | string    | n/a          | entire OPTIONS response                                                                                        |
| registerTime    | integer   | milliseconds | time to complete REGISTER                                                                                      |
| responseCode    | integer   | n/a          | SIP server response code                                                                                       |
| responseTime    | integer   | milliseconds | time to first byte                                                                                             |
| totalTime       | integer   | milliseconds | total time                                                                                                     |
| waitTime        | integer   | milliseconds | time elapsed between completion of request and first byte of response                                          |
| errorType       | string    | n/a          | error type, `None` if there is no error                                                                        |
| problemDetail   | string    | n/a          | error details, if an error was encountered                                                                     |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/voice/sip-server/1193489.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 07 Nov 2018 15:59:16 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1541606400 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-2`

**Body**

`{ "pages": { "current": 1, }, "voice": { "sipMetrics": [ { "agentId": 9765, "agentName": "Oakland, CA (Cogent)", "availability": 100.0, "connectTime": 5, "countryId": "US", "date": "2020-08-29 19:08:02", "dnsTime": 2, "errorType": "None", "numRedirects": 0, "optionsRequest": "OPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 38.140.61.68:55431;branch=z9hG4bKRTzPzMoVh0;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=cGaJDNKQFE\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: oO9WaL3av8@38.140.61.68\r\nCSeq: 3 OPTIONS\r\nContact: <sip:6054@38.140.61.68:55431;transport=tcp>\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n\nOPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 38.140.61.68:55431;branch=z9hG4bKRTzPzMoVh0;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=cGaJDNKQFE\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: oO9WaL3av8@38.140.61.68\r\nCSeq: 4 OPTIONS\r\nContact: <sip:6054@38.140.61.68:55431;transport=tcp>\r\nAuthorization: Digest username=\"al6054\", realm=\"asterisk\", nonce=\"1598728080/4e3bef2c789bdfa45ce9123221e08c8f\", uri=\"sip:6054@voice.sfo2.notarealco.com\", response=\"83c538a39ff766cf75ffd1d62317b442\", algorithm=MD5, cnonce=\"0a4f113b\", opaque=\"748ffa241d840721\", qop=auth, nc=00000001\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n", "optionsResponse": "SIP/2.0 401 Unauthorized\r\nVia: SIP/2.0/TCP 38.140.61.68:55431;rport=55431;received=38.140.61.68;branch=z9hG4bKRTzPzMoVh0\r\nCall-ID: oO9WaL3av8@38.140.61.68\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=cGaJDNKQFE\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKRTzPzMoVh0\r\nCSeq: 3 OPTIONS\r\nWWW-Authenticate: Digest realm=\"asterisk\",nonce=\"1598728080/4e3bef2c789bdfa45ce9123221e08c8f\",opaque=\"748ffa241d840721\",algorithm=md5,qop=\"auth\"\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n\nSIP/2.0 200 OK\r\nVia: SIP/2.0/TCP 38.140.61.68:55431;rport=55431;received=38.140.61.68;branch=z9hG4bKRTzPzMoVh0\r\nCall-ID: oO9WaL3av8@38.140.61.68\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=cGaJDNKQFE\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKRTzPzMoVh0\r\nCSeq: 4 OPTIONS\r\nAccept: application/xpidf+xml, application/cpim-pidf+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/sdp, message/sipfrag;version=2.0\r\nAllow: OPTIONS, REGISTER, SUBSCRIBE, NOTIFY, PUBLISH, INVITE, ACK, BYE, CANCEL, UPDATE, PRACK, MESSAGE, REFER\r\nSupported: 100rel, timer, replaces, norefersub\r\nAccept-Encoding: text/plain\r\nAccept-Language: en\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n", "optionsTime": 13, "permalink": "https://app.thousandeyes.com/view/tests?__a=143292&testId=1085470&roundId=1598728080&agentId=9765", "registerTime": 21, "responseCode": 200, "responseTime": 12, "roundId": 1598728080, "serverIp": "167.71.124.37", "totalTime": 40, "waitTime": 5 }, { "agentId": 14410, "agentName": "San Francisco, CA", "availability": 100.0, "connectTime": 2, "countryId": "US", "date": "2020-08-29 19:08:42", "dnsTime": 1, "errorType": "None", "numRedirects": 0, "optionsRequest": "OPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 64.124.218.217:50485;branch=z9hG4bKchgijI4leu;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=Ab2otkvbE3\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: MAzmInmtZ9@64.124.218.217\r\nCSeq: 3 OPTIONS\r\nContact: <sip:6054@64.124.218.217:50485;transport=tcp>\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n\nOPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 64.124.218.217:50485;branch=z9hG4bKchgijI4leu;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=Ab2otkvbE3\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: MAzmInmtZ9@64.124.218.217\r\nCSeq: 4 OPTIONS\r\nContact: <sip:6054@64.124.218.217:50485;transport=tcp>\r\nAuthorization: Digest username=\"al6054\", realm=\"asterisk\", nonce=\"1598728120/1212c598815ef6f2f393d0f4345ef299\", uri=\"sip:6054@voice.sfo2.notarealco.com\", response=\"4e1b35c54707a30aba4122ef570160a7\", algorithm=MD5, cnonce=\"0a4f113b\", opaque=\"5d52c6d072961833\", qop=auth, nc=00000001\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n", "optionsResponse": "SIP/2.0 401 Unauthorized\r\nVia: SIP/2.0/TCP 64.124.218.217:50485;rport=50485;received=64.124.218.217;branch=z9hG4bKchgijI4leu\r\nCall-ID: MAzmInmtZ9@64.124.218.217\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=Ab2otkvbE3\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKchgijI4leu\r\nCSeq: 3 OPTIONS\r\nWWW-Authenticate: Digest realm=\"asterisk\",nonce=\"1598728120/1212c598815ef6f2f393d0f4345ef299\",opaque=\"5d52c6d072961833\",algorithm=md5,qop=\"auth\"\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n\nSIP/2.0 200 OK\r\nVia: SIP/2.0/TCP 64.124.218.217:50485;rport=50485;received=64.124.218.217;branch=z9hG4bKchgijI4leu\r\nCall-ID: MAzmInmtZ9@64.124.218.217\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=Ab2otkvbE3\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKchgijI4leu\r\nCSeq: 4 OPTIONS\r\nAccept: application/xpidf+xml, application/cpim-pidf+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/sdp, message/sipfrag;version=2.0\r\nAllow: OPTIONS, REGISTER, SUBSCRIBE, NOTIFY, PUBLISH, INVITE, ACK, BYE, CANCEL, UPDATE, PRACK, MESSAGE, REFER\r\nSupported: 100rel, timer, replaces, norefersub\r\nAccept-Encoding: text/plain\r\nAccept-Language: en\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n", "optionsTime": 4, "permalink": "https://app.thousandeyes.com/view/tests?__a=143292&testId=1085470&roundId=1598728080&agentId=14410", "registerTime": 5, "responseCode": 200, "responseTime": 4, "roundId": 1598728080, "serverIp": "167.71.124.37", "totalTime": 12, "waitTime": 2 }, { "agentId": 34, "agentName": "Los Angeles, CA", "availability": 100.0, "connectTime": 10, "countryId": "US", "date": "2020-08-29 19:09:22", "dnsTime": 0, "errorType": "None", "numRedirects": 0, "optionsRequest": "OPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 207.198.106.63:39761;branch=z9hG4bKoAOdZ8LOci;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=XwmtVtDf0o\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: C3KxflK1BY@207.198.106.63\r\nCSeq: 3 OPTIONS\r\nContact: <sip:6054@207.198.106.63:39761;transport=tcp>\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n\nOPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 207.198.106.63:39761;branch=z9hG4bKoAOdZ8LOci;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=XwmtVtDf0o\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: C3KxflK1BY@207.198.106.63\r\nCSeq: 4 OPTIONS\r\nContact: <sip:6054@207.198.106.63:39761;transport=tcp>\r\nAuthorization: Digest username=\"al6054\", realm=\"asterisk\", nonce=\"1598728160/5adc416287c7b55492e3fe24196b7fbb\", uri=\"sip:6054@voice.sfo2.notarealco.com\", response=\"0c20df6f8f4d9a4f0791698f775849df\", algorithm=MD5, cnonce=\"0a4f113b\", opaque=\"341652ef4bac9172\", qop=auth, nc=00000001\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n", "optionsResponse": "SIP/2.0 401 Unauthorized\r\nVia: SIP/2.0/TCP 207.198.106.63:39761;rport=39761;received=207.198.106.63;branch=z9hG4bKoAOdZ8LOci\r\nCall-ID: C3KxflK1BY@207.198.106.63\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=XwmtVtDf0o\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKoAOdZ8LOci\r\nCSeq: 3 OPTIONS\r\nWWW-Authenticate: Digest realm=\"asterisk\",nonce=\"1598728160/5adc416287c7b55492e3fe24196b7fbb\",opaque=\"341652ef4bac9172\",algorithm=md5,qop=\"auth\"\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n\nSIP/2.0 200 OK\r\nVia: SIP/2.0/TCP 207.198.106.63:39761;rport=39761;received=207.198.106.63;branch=z9hG4bKoAOdZ8LOci\r\nCall-ID: C3KxflK1BY@207.198.106.63\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=XwmtVtDf0o\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKoAOdZ8LOci\r\nCSeq: 4 OPTIONS\r\nAccept: application/xpidf+xml, application/cpim-pidf+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/sdp, message/sipfrag;version=2.0\r\nAllow: OPTIONS, REGISTER, SUBSCRIBE, NOTIFY, PUBLISH, INVITE, ACK, BYE, CANCEL, UPDATE, PRACK, MESSAGE, REFER\r\nSupported: 100rel, timer, replaces, norefersub\r\nAccept-Encoding: text/plain\r\nAccept-Language: en\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n", "optionsTime": 22, "permalink": "https://app.thousandeyes.com/view/tests?__a=143292&testId=1085470&roundId=1598728080&agentId=34", "registerTime": 22, "responseCode": 200, "responseTime": 21, "roundId": 1598728080, "serverIp": "167.71.124.37", "totalTime": 55, "waitTime": 11 }, { "agentId": 9765, "agentName": "Oakland, CA (Cogent)", "availability": 100.0, "connectTime": 5, "countryId": "US", "date": "2020-08-29 19:10:02", "dnsTime": 0, "errorType": "None", "numRedirects": 0, "optionsRequest": "OPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 38.140.61.68:53461;branch=z9hG4bKuxJ6plLJ3b;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=JaVFIlZEC7\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: POvr7pS79I@38.140.61.68\r\nCSeq: 3 OPTIONS\r\nContact: <sip:6054@38.140.61.68:53461;transport=tcp>\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n\nOPTIONS sip:6054@voice.sfo2.notarealco.com SIP/2.0\r\nVia: SIP/2.0/TCP 38.140.61.68:53461;branch=z9hG4bKuxJ6plLJ3b;rport\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=JaVFIlZEC7\r\nTo: <sip:6054@voice.sfo2.notarealco.com>\r\nCall-ID: POvr7pS79I@38.140.61.68\r\nCSeq: 4 OPTIONS\r\nContact: <sip:6054@38.140.61.68:53461;transport=tcp>\r\nAuthorization: Digest username=\"al6054\", realm=\"asterisk\", nonce=\"1598728200/dc62d2a240e6a5b6437eb3a6b88678ed\", uri=\"sip:6054@voice.sfo2.notarealco.com\", response=\"6e9b9cc6f5e03239236c58d420c5b47a\", algorithm=MD5, cnonce=\"0a4f113b\", opaque=\"57e5825f493be8b6\", qop=auth, nc=00000001\r\nUser-Agent: ThousandEyes Test Call\r\nAllow: INVITE, ACK, CANCEL, BYE\r\nSupported: outbound, path\r\nMax-Forwards: 70\r\nExpires: 60\r\nContent-Length: 0\r\n\r\n", "optionsResponse": "SIP/2.0 401 Unauthorized\r\nVia: SIP/2.0/TCP 38.140.61.68:53461;rport=53461;received=38.140.61.68;branch=z9hG4bKuxJ6plLJ3b\r\nCall-ID: POvr7pS79I@38.140.61.68\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=JaVFIlZEC7\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKuxJ6plLJ3b\r\nCSeq: 3 OPTIONS\r\nWWW-Authenticate: Digest realm=\"asterisk\",nonce=\"1598728200/dc62d2a240e6a5b6437eb3a6b88678ed\",opaque=\"57e5825f493be8b6\",algorithm=md5,qop=\"auth\"\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n\nSIP/2.0 200 OK\r\nVia: SIP/2.0/TCP 38.140.61.68:53461;rport=53461;received=38.140.61.68;branch=z9hG4bKuxJ6plLJ3b\r\nCall-ID: POvr7pS79I@38.140.61.68\r\nFrom: <sip:6054@voice.sfo2.notarealco.com>;tag=JaVFIlZEC7\r\nTo: <sip:6054@voice.sfo2.notarealco.com>;tag=z9hG4bKuxJ6plLJ3b\r\nCSeq: 4 OPTIONS\r\nAccept: application/xpidf+xml, application/cpim-pidf+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/simple-message-summary, application/pidf+xml, application/dialog-info+xml, application/sdp, message/sipfrag;version=2.0\r\nAllow: OPTIONS, REGISTER, SUBSCRIBE, NOTIFY, PUBLISH, INVITE, ACK, BYE, CANCEL, UPDATE, PRACK, MESSAGE, REFER\r\nSupported: 100rel, timer, replaces, norefersub\r\nAccept-Encoding: text/plain\r\nAccept-Language: en\r\nServer: Asterisk PBX 16.4.0\r\nContent-Length: 0\r\n\r\n", "optionsTime": 13, "permalink": "https://app.thousandeyes.com/view/tests?__a=143292&testId=1085470&roundId=1598728200&agentId=9765", "registerTime": 19, "responseCode": 200, "responseTime": 14, "roundId": 1598728200, "serverIp": "167.71.124.37", "totalTime": 38, "waitTime": 8 } ], "test": { "alertsEnabled": 0, "apiLinks": [...], "authUser": "al6054", "bandwidthMeasurements": 0, "bgpMeasurements": 1, "createdBy": "ThousandEyes (noreply@thousandeyes.com)", "createdDate": "2019-09-12 01:57:54", "enabled": 1, "interval": 120, "ipv6Policy": "USE_AGENT_POLICY", "liveShare": 0, "modifiedBy": "ThousandEyes (noreply@thousandeyes.com)", "modifiedDate": "2020-06-30 04:19:25", "mtuMeasurements": 1, "networkMeasurements": 1, "numPathTraces": 3, "optionsRegex": "", "pathTraceMode": "classic", "port": 6061, "probeMode": "AUTO", "protocol": "TCP", "registerEnabled": 1, "savedEvent": 0, "server": "voice.sfo2.notarealco.com:6061", "sipProxy": "", "sipRegistrar": "voice.sfo2.notarealco.com", "sipTargetTime": 1000, "sipTimeLimit": 5, "testId": 1085470, "testName": "SIP - IPv4 - TCP: voice.sfo2.notarealco.com - ext 6054", "type": "sip-server", "usePublicBgp": 1, "user": "6054" } } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/voice/rtp-stream/{testId}` (Voice) RTP stream](broken-reference)

Returns voice RTP stream metrics (loss, latency, jitter, MOS score) from each agent, for each _roundId_ in the requested window. A **time frame** must be specified, or the current round of data will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` (Optional) specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` (Optional) specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` (Optional) specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` (Required) the ID of the RTP Stream test for which you wish to retrieve data
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field       | Data Type | Units        | Notes                                                              |
| ----------- | --------- | ------------ | ------------------------------------------------------------------ |
| agentId     | integer   | n/a          | source agent unique Id, from `/agents` endpoint                    |
| agentName   | string    | n/a          | display name of the source agent                                   |
| serverIp    | string    | n/a          | target agent IP address                                            |
| countryId   | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                       |
| date        | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                        |
| roundId     | long      | seconds      | epoch time (seconds) indicating the start time of the round        |
| permalink   | url       | n/a          | link to jump to this result in the front end                       |
| dscp        | string    | n/a          | DSCP value received by the server from the agent                   |
| dscpName    | string    | n/a          | name of DSCP value received by the server from the agent           |
| mos         | float     | n/a          | Mean opinion score for agent’s stream                              |
| codecName   | string    | n/a          | name of codec used by agent                                        |
| codecMaxMos | float     | n/a          | maximum value of Mean Opinion Score based on codec selection       |
| loss        | float     | percentage   | percentage value of packets sent from agent not received by server |
| discards    | integer   | n/a          | number of packets discarded                                        |
| latency     | integer   | milliseconds | time to send packets from source to server                         |
| pdv         | float     | milliseconds | variation in packet delay, measured in milliseconds                |
| errorDetail | string    | n/a          | error details, if an error was encountered.                        |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/voice/rtp-stream/1004633.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 10 Nov 2018 16:43:10 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 229 X-Organization-Rate-Limit-Reset: 1541868240 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "pages": { "current": 1 }, "voice": { "metrics": [ { "agentId": 58, "agentName": "Cairo, Egypt", "codecMaxMos": 4.41, "codecName": "G.711 @ 64 Kbps", "countryId": "EG", "date": "2020-09-09 04:58:06", "discards": 0.0, "dscp": 46, "dscpName": "EF (DSCP 46)", "latency": 103, "loss": 0.0, "mos": 4.351024, "pdv": 1, "permalink": "https://app.thousandeyes.com/voice/metrics?__a=75&testId=1661929&roundId=1599627480&agentId=58", "roundId": 1599627480, "serverIp": "172.97.102.37" } ], "test": { "alertsEnabled": 0, "apiLinks": [...], "bgpMeasurements": 0, "codec": "G.711 @ 64 Kbps", "codecId": 0, "createdBy": "ThousandEyes (support@thousandeyes.com)", "createdDate": "2020-09-09 02:56:03", "dscp": "EF (DSCP 46)", "dscpId": 46, "duration": 5, "enabled": 1, "interval": 120, "jitterBuffer": 40, "liveShare": 0, "numPathTraces": 3, "savedEvent": 0, "server": "a1-docker1-abq.ag1.thousandeyes.com:49152", "targetAgentId": 8641, "testId": 1661929, "testName": "RTP-Stream", "type": "voice", "usePublicBgp": 1 } } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
