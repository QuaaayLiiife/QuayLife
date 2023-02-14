# Endpoint Test Data

### Endpoint Test Data

[`GET /v6/endpoint-data/tests/net/metrics/{testId}` Scheduled Tests (Network) End-to-End metrics](broken-reference)

Returns network metrics (loss, latency, jitter and bandwidth) from each endpoint agent, for each _roundId_ in the requested window. A **time frame** must be specified, or the most recent round within last 2 hours will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the endpoint scheduled test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field         | Data Type | Units        | Notes                                                         |
| ------------- | --------- | ------------ | ------------------------------------------------------------- |
| agentId       | string    | n/a          | Unique ID of endpoint agent, from `/endpoint-agents` endpoint |
| avgLatency    | float     | milliseconds | Average RTT for packets sent to destination                   |
| errorDetails  | string    | n/a          | Error details, if an error was encountered                    |
| jitter        | float     | milliseconds | Standard deviation of latency                                 |
| loss          | float     | percentage   | % of packets not reaching destination                         |
| maxLatency    | integer   | milliseconds | Maxmimum RTT for packets sent to destination                  |
| minLatency    | integer   | milliseconds | Minimum RTT for packets sent to destination                   |
| permalink     | url       | n/a          | Link to jump to this result in the front end                  |
| roundId       | long      | seconds      | Epoch time (seconds) indicating the start time of the round   |
| serverIp      | string    | n/a          | IP address of target server                                   |
| systemMetrics | object    | n/a          | Contains system metrics such as CPU and physical memory usage |

`systemMetrics` object has the following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/tests/net/metrics/273.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 21:19:54 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1535232000 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-2`

**Body**

`{ "endpointNet": { "endpointTest": {...}, "metrics": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "avgLatency": 10.0, "jitter": 1.0, "loss": 0.0, "maxLatency": 13.0, "minLatency": 7.0, "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowNetworkTest&testId=273&roundId=1535228220", "roundId": 1535228220, "serverIp": "185.199.108.153", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/tests/net/path-vis/{testId}` Scheduled Tests (Network) Path visualization](broken-reference)

Returns a summary of the path visualization data collected from each endpoint agent to the destination. In each path visualization attempt, one attempt is made to reach the destination. Each set of data is summarized, based on response time, number of hops, and response time to the target. A **time frame** must be specified, or the most recent round within last 2 hours will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field                  | Data Type | Units   | Notes                                                                         |
| ---------------------- | --------- | ------- | ----------------------------------------------------------------------------- |
| agentId                | string    | n/a     | Unique ID of agent, from `/endpoint-agents` endpoint                          |
| location               | string    | n/a     | Geographic location of the endpoint agent                                     |
| permalink              | url       | n/a     | Link to jump to this result in the front end                                  |
| roundId                | long      | seconds | Epoch time (seconds) indicating the start time of the round                   |
| server                 | url       | n/a     | Target server, including port                                                 |
| serverIp               | string    | n/a     | IP address of target server                                                   |
| sourceIp               | string    | n/a     | IP address of source endpoint agent                                           |
| sourcePrefix           | string    | n/a     | IP prefix of source agent                                                     |
| endpoints              | array     | n/a     | Shows all iterations of path trace, with each iteration specified by a pathId |
| endpoints.ipAddress    | string    | n/a     | Destination                                                                   |
| endpoints.numberOfHops | integer   | n/a     | Number of hops for path trace to destination                                  |
| endpoints.pathId       | string    | n/a     | Unique ID of path trace                                                       |
| endpoints.responseTime | integer   | n/a     | RTT of the path trace to the destination                                      |
| systemMetrics          | object    | n/a     | Contains system metrics such as CPU and physical memory usage                 |
| vpnProfile             | object    | n/a     | Contains information about the currently active VPN                           |

`systemMetrics` object has the following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

`vpnProfile` object has the following properties:

| Field                 | Data Type | Notes                                                                         |
| --------------------- | --------- | ----------------------------------------------------------------------------- |
| vpnClientAddresses    | array     | List of private IP addresses that the VPN server assigned to the device       |
| vpnClientNetworkRange | array     | List of private networks that the VPN server assigned to the device           |
| vpnGatewayAddress     | string    | IP address of the VPN gateway                                                 |
| vpnType               | string    | Name of the VPN provider. For example, “CiscoAnyConnect” or “ZscalerInternet” |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/tests/net/path-vis/273.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 29 Aug 2018 14:01:39 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1535551320 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointNet": { "endpointTest": {...}, "pathVis": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "endpoints": [ { "ipAddress": "185.199.111.153", "numberOfHops": 8, "pathId": "8498006760529413427021933451903980591243082534558334817588690338427397277769705862118603451313420092120640807102236650497915440", "responseTime": 5 } ], "location": "San Francisco Area", "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowNetworkTest&testId=273&roundId=1535550480", "roundId": 1535550480, "server": "developer.thousandeyes.com:443", "serverIp": "185.199.111.153", "sourceIp": "10.100.10.35", "sourcePrefix": "38.122.6.64/30", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 }, "vpnProfile": { "vpnType": "CiscoAnyConnect", "vpnGatewayAddress": "144.254.221.38" } }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/tests/net/path-vis/{testId}/{agentId}/{roundId}` Scheduled Tests (Network) Detailed path trace](broken-reference)

Returns a hop-by-hop summary of the path trace data collected during path visualization. In each round, one path discovery attempt is made to reach the destination. The entire path is returned. A `roundId` must be specified.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

Required parameters:

* `{testId}` the ID of the test you wish to retrieve
* `{agentId}` the ID of the endpoint agent from which you wish to obtain data
* `{roundId}` the round ID for which you wish to obtain data. Equals the beginning of the testing round, in epoch time format.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

* Each route should start with a hop of 1
* Where a hop number is missing from response data, this is an indication that a star (\*) response was returned in the path trace attempt for that hop.

| Field                   | Data Type | Units        | Notes                                                                       |
| ----------------------- | --------- | ------------ | --------------------------------------------------------------------------- |
| agentId                 | string    | n/a          | Unique ID of agent, from `/endpoint-agents` endpoint                        |
| permalink               | url       | n/a          | Link to jump to this result in the front end                                |
| roundId                 | long      | seconds      | Epoch time (seconds) indicating the start time of the round                 |
| server                  | url       | n/a          | Target server, including port                                               |
| serverIp                | string    | n/a          | IP address of target server                                                 |
| sourceIp                | string    | n/a          | IP address of source endpoint agent                                         |
| sourcePrefix            | string    | n/a          | IP prefix of source agent                                                   |
| routes                  | array     | n/a          | Shows an iteration of path trace, with each iteration specified by a pathId |
| routes.pathId           | string    | n/a          | Unique ID of path trace                                                     |
| routes.hops             | array     | n/a          | Array of hop objects indicating each step in the traceroute                 |
| routes.hops.hop         | integer   | n/a          | Index of hop                                                                |
| routes.hops.ipAddress   | string    | n/a          | IP address of the hop                                                       |
| routes.hop.prefix       | string    | n/a          | Prefix of IP address shown in CIDR                                          |
| routes.hop.rdns         | string    | n/a          | Reverse DNS entry of IP, if available                                       |
| routes.hop.network      | string    | n/a          | Autonomous System originating the prefix                                    |
| routes.hop.responseTime | integer   | milliseconds | RTT to the hop’s IP                                                         |
| routes.hop.location     | string    | n/a          | Location information for the hop                                            |
| systemMetrics           | object    | n/a          | Contains system metrics such as CPU and physical memory usage               |
| vpnProfile              | object    | n/a          | Contains information about the currently active VPN                         |

`systemMetrics` object has the following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

`vpnProfile` object has the following properties:

| Field                 | Data Type | Notes                                                                         |
| --------------------- | --------- | ----------------------------------------------------------------------------- |
| vpnClientAddresses    | array     | List of private IP addresses that the VPN server assigned to the device       |
| vpnClientNetworkRange | array     | List of private networks that the VPN server assigned to the device           |
| vpnGatewayAddress     | string    | IP address of the VPN gateway                                                 |
| vpnType               | string    | Name of the VPN provider. For example, “CiscoAnyConnect” or “ZscalerInternet” |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/tests/net/path-vis/273/1cf6d996-2400-4724-a805-2de78756c209/1535551380.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 29 Aug 2018 14:08:20 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1535551740 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-5`

**Body**

`{ "endpointNet": { "endpointTest": {...}, "pathVis": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowNetworkTest&testId=273&roundId=1535551380", "roundId": 1535551380, "routes": [ { "hops": [ { "hop": 1, "ipAddress": "10.100.10.1", "rdns": "vlan10.fw1.sfo1.o.thousandeyes.com", "responseTime": 3 }, { "hop": 2, "ipAddress": "38.122.6.65", "location": "San Francisco, California, US", "network": "Cogent Communications (AS 174)", "prefix": "38.0.0.0/8", "rdns": "gi0-0-0-4.nr11.b001920-0.sfo01.atlas.cogentco.com", "responseTime": 4 }, { "hop": 3, "ipAddress": "154.24.7.73", "location": "San Francisco, California, US", "network": "Cogent Communications (AS 174)", "prefix": "154.24.0.0/13", "rdns": "gi0-0-0-6.agr22.sfo01.atlas.cogentco.com", "responseTime": 3 }, { "hop": 4, "ipAddress": "154.54.30.221", "location": "San Francisco, California, US", "network": "Cogent Communications (AS 174)", "prefix": "154.48.0.0/12", "rdns": "be2905.ccr22.sfo01.atlas.cogentco.com", "responseTime": 4 }, { "hop": 5, "ipAddress": "154.54.0.178", "location": "San Jose, California, US", "network": "Cogent Communications (AS 174)", "prefix": "154.48.0.0/12", "rdns": "be2016.ccr31.sjc04.atlas.cogentco.com", "responseTime": 4 }, { "hop": 6, "ipAddress": "62.115.34.73", "location": "San Jose, California, US", "network": "TeliaNet Global Network (AS 1299)", "prefix": "62.115.0.0/16", "rdns": "palo-b1-link.telia.net", "responseTime": 6 }, { "hop": 8, "ipAddress": "185.199.111.153", "location": "San Jose, California, US", "network": "Fastly (AS 54113)", "prefix": "185.199.111.0/24", "rdns": "185.199.111.153", "responseTime": 4 } ], "pathId": "8498006760529413427021933451903980591243082534558334817588690338427397277769705862118603451313420092120640807102237745714575920" } ], "server": "developer.thousandeyes.com:443", "serverIp": "185.199.111.153", "sourceIp": "10.100.10.35", "sourcePrefix": "38.122.6.64/30", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 }, "vpnProfile": { "vpnType": "CiscoAnyConnect", "vpnGatewayAddress": "144.254.221.38" } } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/tests/web/http-server/{testId}` Scheduled Tests (Web) HTTP server](broken-reference)

Returns response code and response times, as well as component-level (DNS, Connect, Wait and Receive) timing for the load of an object over HTTP.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the HTTP Server (or page load) test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field           | Data Type | Units        | Notes                                                                 |
| --------------- | --------- | ------------ | --------------------------------------------------------------------- |
| agentId         | string    | n/a          | Unique ID of agent, from `/endpoint-agents` endpoint                  |
| connectTime     | integer   | milliseconds | Time required to establish a TCP connection to the server             |
| dnsTime         | integer   | milliseconds | Time required to resolve DNS                                          |
| errorType       | string    | n/a          | Type of error encountered; corresponds to phase of connection         |
| errorDetails    | string    | n/a          | Error details, if an error was encountered                            |
| numRedirects    | integer   | n/a          | Number of redirects                                                   |
| permalink       | url       | n/a          | Link to jump to this result in the front end                          |
| receiveTime     | integer   | milliseconds | Elapsed time between first and last byte of response                  |
| redirectTime    | integer   | milliseconds | Cumulative redirect timing                                            |
| requestHeaders  | string    | n/a          | CRLF-delimited list of request headers in header: value format        |
| responseCode    | integer   | n/a          | Code of HTTP response                                                 |
| responseHeaders | string    | n/a          | CRLF-delimited list of response headers in header: value format       |
| responseTime    | integer   | milliseconds | Time to first byte                                                    |
| roundId         | long      | seconds      | Epoch time (seconds) indicating the start time of the round           |
| serverIp        | string    | n/a          | IP address of destination server                                      |
| sslTime         | integer   | milliseconds | Time to negotiate SSL/TLS                                             |
| totalTime       | integer   | milliseconds | Response time + receive time                                          |
| waitTime        | integer   | milliseconds | Time elapsed between completion of request and first byte of response |
| wireSize        | float     | bytes        | Size of content, in bytes                                             |
| systemMetrics   | object    | n/a          | Contains system metrics such as CPU and physical memory usage         |

`systemMetrics` object has the following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/tests/web/http-server/273.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 29 Aug 2018 14:28:18 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535552940 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-4`

**Body**

`{ "endpointWeb": "endpointTest": {...}, "httpServer": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "connectTime": 12, "dnsTime": 6, "errorType": "None", "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowHttp&testId=273&roundId=1535551800", "receiveTime": 17, "requestHeaders": "GET / HTTP/1.1\r\n\nHost: developer.thousandeyes.com\r\n\nAuthorization: Basic (removed)\r\n\nUser-Agent: curl/\r\n\nAccept: */*\r\n\nX-ThousandEyes-Endpoint-Agent: yes\r\n", "responseCode": 200, "responseHeaders": "HTTP/1.1 200 OK\r\n\nServer: GitHub.com\r\n\nContent-Type: text/html; charset=utf-8\r\n\nLast-Modified: Thu, 23 Aug 2018 14:16:48 GMT\r\n\nETag: \"5b7ec1d0-14f4f\"\r\n\nAccess-Control-Allow-Origin: *\r\n\nExpires: Thu, 23 Aug 2018 14:37:00 GMT\r\n\nCache-Control: max-age=600\r\n\nX-GitHub-Request-Id: F86C:9AD2:7ABF9:89530:5B7EC42E\r\n\nContent-Length: 85839\r\n\nAccept-Ranges: bytes\r\n\nDate: Wed, 29 Aug 2018 14:10:00 GMT\r\n\nVia: 1.1 varnish\r\n\nAge: 480\r\n\nConnection: keep-alive\r\n\nX-Served-By: cache-pao17433-PAO\r\n\nX-Cache: HIT\r\n\nX-Cache-Hits: 1\r\n\nX-Timer: S1535551800.182689,VS0,VE1\r\n\nVary: Accept-Encoding\r\n\nX-Fastly-Request-ID: a665076014deec318792ec930c9cd6ae62fd2ae3\r\n", "responseTime": 46, "roundId": 1535551800, "serverIp": "185.199.111.153", "sslTime": 11, "totalTime": 63, "waitTime": 16, "wireSize": 86462, "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/automated-session-tests/net/metrics/{testId}` Automated Session Tests End-to-End metrics](broken-reference)

Returns network metrics (loss, latency, jitter and bandwidth) from each endpoint agent, for each _roundId_ in the requested window. A **time frame** must be specified, or the most recent round within last 2 hours will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the endpoint automated session test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field         | Data Type | Units        | Notes                                                         |
| ------------- | --------- | ------------ | ------------------------------------------------------------- |
| agentId       | string    | n/a          | Unique ID of endpoint agent, from `/endpoint-agents` endpoint |
| avgLatency    | float     | milliseconds | Average RTT for packets sent to destination                   |
| errorDetails  | string    | n/a          | Error details, if an error was encountered                    |
| jitter        | float     | milliseconds | Standard deviation of latency                                 |
| loss          | float     | percentage   | % of packets not reaching destination                         |
| maxLatency    | integer   | milliseconds | Maxmimum RTT for packets sent to destination                  |
| minLatency    | integer   | milliseconds | Minimum RTT for packets sent to destination                   |
| permalink     | url       | n/a          | Link to jump to this result in the front end                  |
| roundId       | long      | seconds      | Epoch time (seconds) indicating the start time of the round   |
| serverIp      | string    | n/a          | IP address of target server                                   |
| systemMetrics | object    | n/a          | Contains system metrics such as CPU and physical memory usage |
| application   | string    | n/a          | Monitored application, can be one of WEBEX, ZOOM, MSTEAMS     |
| webex         | object    | n/a          | Contains metadata of a Webex test e.g. Webex conference id    |

`systemMetrics` object has the following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/automated-session-tests/net/metrics/273.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 21:19:54 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1535232000 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-2`

**Body**

`{ "endpointAutomatedSessionTestNet": { "automatedSessionTest": {...}, "metrics": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "avgLatency": 10.0, "jitter": 1.0, "loss": 0.0, "maxLatency": 13.0, "minLatency": 7.0, "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowNetworkTest&testId=273&roundId=1535228220", "roundId": 1535228220, "serverIp": "185.199.108.153", "webex": { "conferenceId": "225817074608419375" "correlationId": "22581707460321454" }, "application": "WEBEX", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/automated-session-tests/net/path-vis/{testId}` Automated Session Tests Path visualization](broken-reference)

Returns a summary of the path visualization data collected from each endpoint agent to the destination. In each path visualization attempt, one attempt is made to reach the destination. Each set of data is summarized, based on response time, number of hops, and response time to the target. A **time frame** must be specified, or the most recent round within last 2 hours will be returned.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field                  | Data Type | Units   | Notes                                                                         |
| ---------------------- | --------- | ------- | ----------------------------------------------------------------------------- |
| agentId                | string    | n/a     | Unique ID of agent, from `/endpoint-agents` endpoint                          |
| location               | string    | n/a     | Geographic location of the endpoint agent                                     |
| permalink              | url       | n/a     | Link to jump to this result in the front end                                  |
| roundId                | long      | seconds | Epoch time (seconds) indicating the start time of the round                   |
| server                 | url       | n/a     | Target server, including port                                                 |
| serverIp               | string    | n/a     | IP address of target server                                                   |
| sourceIp               | string    | n/a     | IP address of source endpoint agent                                           |
| sourcePrefix           | string    | n/a     | IP prefix of source agent                                                     |
| endpoints              | array     | n/a     | Shows all iterations of path trace, with each iteration specified by a pathId |
| endpoints.ipAddress    | string    | n/a     | Destination                                                                   |
| endpoints.numberOfHops | integer   | n/a     | Number of hops for path trace to destination                                  |
| endpoints.pathId       | string    | n/a     | Unique ID of path trace                                                       |
| endpoints.responseTime | integer   | n/a     | RTT of the path trace to the destination                                      |
| systemMetrics          | object    | n/a     | Contains system metrics such as CPU and physical memory usage                 |
| application            | string    | n/a     | Monitored application, can be one of WEBEX, ZOOM, MSTEAMS                     |
| webex                  | object    | n/a     | Contains metadata of a Webex test e.g. Webex conference id                    |
| vpnProfile             | object    | n/a     | Contains information about the currently active VPN                           |

`systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

`vpnProfile` object has the following properties:

| Field                 | Data Type | Notes                                                                         |
| --------------------- | --------- | ----------------------------------------------------------------------------- |
| vpnClientAddresses    | array     | List of private IP addresses that the VPN server assigned to the device       |
| vpnClientNetworkRange | array     | List of private networks that the VPN server assigned to the device           |
| vpnGatewayAddress     | string    | IP address of the VPN gateway                                                 |
| vpnType               | string    | Name of the VPN provider. For example, “CiscoAnyConnect” or “ZscalerInternet” |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/automated-session-tests/net/path-vis/273.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 29 Aug 2018 14:01:39 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1535551320 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAutomatedSessionTestNet": { "automatedSessionTest": {...}, "pathVis": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "endpoints": [ { "ipAddress": "185.199.111.153", "numberOfHops": 8, "pathId": "8498006760529413427021933451903980591243082534558334817588690338427397277769705862118603451313420092120640807102236650497915440", "responseTime": 5 } ], "location": "San Francisco Area", "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowNetworkTest&testId=273&roundId=1535550480", "roundId": 1535550480, "server": "developer.thousandeyes.com:443", "serverIp": "185.199.111.153", "sourceIp": "10.100.10.35", "sourcePrefix": "38.122.6.64/30", "webex": { "conferenceId": "225817074608419375" "correlationId": "22581707460321454" }, "application": "WEBEX", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 }, "vpnProfile": { "vpnType": "CiscoAnyConnect", "vpnGatewayAddress": "144.254.221.38" } }, ... ] }, "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/automated-session-tests/net/path-vis/{testId}/{agentId}/{roundId}` Automated Session Tests Detailed path trace](broken-reference)

Returns a hop-by-hop summary of the path trace data collected during path visualization. In each round, one path discovery attempt is made to reach the destination. The entire path is returned. A `roundId` must be specified.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

Required parameters:

* `{testId}` the ID of the test you wish to retrieve
* `{agentId}` the ID of the endpoint agent from which you wish to obtain data
* `{roundId}` the round ID for which you wish to obtain data. Equals the beginning of the testing round, in epoch time format.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

* Each route should start with a hop of 1
* Where a hop number is missing from response data, this is an indication that a star (\*) response was returned in the path trace attempt for that hop.

| Field                    | Data Type | Units        | Notes                                                                       |
| ------------------------ | --------- | ------------ | --------------------------------------------------------------------------- |
| agentId                  | integer   | n/a          | Unique ID of agent, from `/endpoint-agents` endpoint                        |
| permalink                | url       | n/a          | Link to jump to this result in the front end                                |
| roundId                  | long      | seconds      | Epoch time (seconds) indicating the start time of the round                 |
| server                   | url       | n/a          | Target server, including port                                               |
| serverIp                 | string    | n/a          | IP address of target server                                                 |
| sourceIp                 | string    | n/a          | IP address of source endpoint agent                                         |
| sourcePrefix             | string    | n/a          | IP prefix of source agent                                                   |
| routes                   | array     | n/a          | Shows an iteration of path trace, with each iteration specified by a pathId |
| routes.pathId            | string    | n/a          | Unique ID of path trace                                                     |
| routes.hops              | array     | n/a          | Array of hop objects indicating each step in the traceroute                 |
| routes.hops.hop          | integer   | n/a          | Index of hop                                                                |
| routes.hops.ipAddress    | string    | n/a          | IP address of the hop                                                       |
| routes.hops.prefix       | string    | n/a          | Prefix of IP address shown in CIDR                                          |
| routes.hops.rdns         | string    | n/a          | Reverse DNS entry of IP, if available                                       |
| routes.hops.network      | string    | n/a          | Autonomous System originating the prefix                                    |
| routes.hops.responseTime | integer   | milliseconds | RTT to the hop’s IP                                                         |
| routes.hops.location     | string    | n/a          | Location information for the hop                                            |
| systemMetrics            | object    | n/a          | Contains system metrics such as CPU and physical memory usage               |
| vpnProfile               | object    | n/a          | Contains information about the currently active VPN                         |

`systemMetrics` object has the following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | Time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | Time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | Contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | Contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | Total physical memory of the system                                       |

`cpuUtilization` object has the following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | Minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | Maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | Mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | Median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | Standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | The number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has the following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | Minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | Maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | Mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | Median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | Standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | The number of collected samples over the monitored period            |

`vpnProfile` object has the following properties:

| Field                 | Data Type | Notes                                                                         |
| --------------------- | --------- | ----------------------------------------------------------------------------- |
| vpnClientAddresses    | array     | List of private IP addresses that the VPN server assigned to the device       |
| vpnClientNetworkRange | array     | List of private networks that the VPN server assigned to the device           |
| vpnGatewayAddress     | string    | IP address of the VPN gateway                                                 |
| vpnType               | string    | Name of the VPN provider. For example, “CiscoAnyConnect” or “ZscalerInternet” |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-data/automated-session-tests/net/path-vis/273/1cf6d996-2400-4724-a805-2de78756c209/1535551380.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Wed, 29 Aug 2018 14:08:20 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1535551740 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-5`

**Body**

`{ "endpointAutomatedSessionTestNet": { "automatedSessionTest": {...}, "pathVis": [ { "agentId": "1cf6d996-2400-4724-a805-2de78756c209", "permalink": "https://app.thousandeyes.com/view/endpoint-agent?__a=160&scenarioId=eyebrowNetworkTest&testId=273&roundId=1535551380", "roundId": 1535551380, "routes": [ { "hops": [ { "hop": 1, "ipAddress": "10.100.10.1", "rdns": "vlan10.fw1.sfo1.o.thousandeyes.com", "responseTime": 3 }, { "hop": 2, "ipAddress": "38.122.6.65", "location": "San Francisco, California, US", "network": "Cogent Communications (AS 174)", "prefix": "38.0.0.0/8", "rdns": "gi0-0-0-4.nr11.b001920-0.sfo01.atlas.cogentco.com", "responseTime": 4 }, { "hop": 3, "ipAddress": "154.24.7.73", "location": "San Francisco, California, US", "network": "Cogent Communications (AS 174)", "prefix": "154.24.0.0/13", "rdns": "gi0-0-0-6.agr22.sfo01.atlas.cogentco.com", "responseTime": 3 }, { "hop": 4, "ipAddress": "154.54.30.221", "location": "San Francisco, California, US", "network": "Cogent Communications (AS 174)", "prefix": "154.48.0.0/12", "rdns": "be2905.ccr22.sfo01.atlas.cogentco.com", "responseTime": 4 }, { "hop": 5, "ipAddress": "154.54.0.178", "location": "San Jose, California, US", "network": "Cogent Communications (AS 174)", "prefix": "154.48.0.0/12", "rdns": "be2016.ccr31.sjc04.atlas.cogentco.com", "responseTime": 4 }, { "hop": 6, "ipAddress": "62.115.34.73", "location": "San Jose, California, US", "network": "TeliaNet Global Network (AS 1299)", "prefix": "62.115.0.0/16", "rdns": "palo-b1-link.telia.net", "responseTime": 6 }, { "hop": 8, "ipAddress": "185.199.111.153", "location": "San Jose, California, US", "network": "Fastly (AS 54113)", "prefix": "185.199.111.0/24", "rdns": "185.199.111.153", "responseTime": 4 } ], "pathId": "8498006760529413427021933451903980591243082534558334817588690338427397277769705862118603451313420092120640807102237745714575920" } ], "server": "developer.thousandeyes.com:443", "serverIp": "185.199.111.153", "sourceIp": "10.100.10.35", "sourcePrefix": "38.122.6.64/30", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 }, "vpnProfile": { "vpnType": "CiscoAnyConnect", "vpnGatewayAddress": "144.254.221.38" } } ] } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
