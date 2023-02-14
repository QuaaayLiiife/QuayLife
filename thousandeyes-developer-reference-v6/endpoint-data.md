# Endpoint Data

### Endpoint Data

[`GET POST /v6/endpoint-data/user-sessions` Endpoint user session list](broken-reference)

Returns a list of all endpoint user sessions. Sessions from the last round are provided unless an explicit start and end is provided with `from`, `to` or `window` optional parameters.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `page={pageNo}` this parameter is going to be deprecated - please rely on the URL in the `pages[next]` element included in the response. See [Pagination](https://developer.thousandeyes.com/v6/#/pagination) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Optional Filtering <a href="#optional_filtering" id="optional_filtering"></a>

`/endpoint-data` endpoints support optional filtering. See [Endpoint Data Filtering](broken-reference) for more information.

#### Request <a href="#request" id="request"></a>

* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/user-sessions.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object. `userSessions` parameter returns an array of endpoint user sessions, either the latest sessions, or based on the time range specified. Each entry represents an endpoint user session.

| Field           | Data Type | Units               | Notes                                                                                                                                                                                                                                                          |
| --------------- | --------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId         | string    | n/a                 | endpoint agent ID                                                                                                                                                                                                                                              |
| committed       | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when endpoint user session was committed to the controller; all dates are UTC                                                                                                                                                                    |
| date            | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when endpoint user session took place; all dates are UTC                                                                                                                                                                                         |
| experienceScore | number    | 0-1                 | score rating a user’s experience when loading a particular page, from 0 (the worst) to 1 (the best). [More details](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/viewing-data/endpoint-agent-views-reference#user-experience-score) |
| numberOfPages   | integer   | n/a                 | number of web pages visited on target website                                                                                                                                                                                                                  |
| orgName         | string    | n/a                 | name of the AS organization `sourceAddr` belongs to                                                                                                                                                                                                            |
| permalink       | string    | n/a                 | hyperlink to endpoint user session details in ThousandEyes Application                                                                                                                                                                                         |
| port            | integer   | n/a                 | port used to visit target website                                                                                                                                                                                                                              |
| protocol        | string    | n/a                 | protocol used to visit target website                                                                                                                                                                                                                          |
| roundId         | integer   | n/a                 | endpoint user session round ID                                                                                                                                                                                                                                 |
| sourceAddr      | string    | n/a                 | public IP address of the endpoint agent during the session                                                                                                                                                                                                     |
| userSessionId   | string    | n/a                 | endpoint user session ID; each endpoint user session occurrence has a unique ID                                                                                                                                                                                |
| visitedSite     | string    | n/a                 | domain used to visit target website                                                                                                                                                                                                                            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 13:41:02 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1490622120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "userSessions": [ { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "committed": "2017-03-22 11:58:44", "date": "2017-03-22 11:58:42", "numberOfPages": 1, "orgName": "T-2 Access Network", "permalink": "https://app.thousandeyes.com/view/endpoint-agent/?roundId=1490529480&scenarioId=sessionDetails&binSize=300000&__aid=7625", "port": 80, "protocol": "http", "roundId": 1490529480, "sourceAddr": "84.255.241.1", "userSessionId": "07625:1490529480:aVDViw0i", "visitedSite": "thousandeyes.com" }, { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "committed": "2017-03-22 11:58:46", "date": "2017-03-22 11:58:43", "numberOfPages": 2, "orgName": "T-2 Access Network", "permalink": "https://app.thousandeyes.com/view/endpoint-agent/?roundId=1490529480&scenarioId=sessionDetails&binSize=300000&__aid=7625", "port": 443, "protocol": "https", "roundId": 1490529480, "sourceAddr": "84.255.241.1", "userSessionId": "07625:1490529480:h3qJQTpl", "visitedSite": "www.thousandeyes.com" } [...] } "pages": { "current": 1 } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/user-sessions/{sessionId}` Endpoint user session details](broken-reference)

Returns details for an endpoint user session

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* {sessionId} corresponds to the id of a endpoint user sessions, see the Endpoint user session list endpoint for a listing of endpoint user sessions.
* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/user-sessions/07625:1490529480:h3qJQTpl.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed data of an endpoint user session.

| Field           | Data Type | Units               | Notes                                                                                                                                                                                                                                                          |
| --------------- | --------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId         | string    | n/a                 | endpoint agent ID                                                                                                                                                                                                                                              |
| browser         | object    | n/a                 | object contains two string parameters, `name` and `version` of the browser                                                                                                                                                                                     |
| committed       | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when endpoint user session was committed to the controller; all dates are UTC                                                                                                                                                                    |
| coordinates     | object    | n/a                 | object contains approximate GPS location of the endpoint agent, based on endpoint agent’s public IP address; `latitude` and `longitude` are numeric representations of GPS coordinates, `location` is a string representing named geographical location        |
| date            | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when endpoint user session took place; all dates are UTC                                                                                                                                                                                         |
| experienceScore | number    | 0-1                 | score rating a user’s experience when loading a particular page, from 0 (the worst) to 1 (the best). [More details](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/viewing-data/endpoint-agent-views-reference#user-experience-score) |
| network         | object    | n/a                 | object contains details about network profile and conditions during session                                                                                                                                                                                    |
| numberOfPages   | integer   | n/a                 | number of web pages visited on target website                                                                                                                                                                                                                  |
| orgName         | string    | n/a                 | name of the AS organization `sourceAddr` belongs to                                                                                                                                                                                                            |
| pages           | array     | n/a                 | array of objects containing details about web pages visited during session; each object represents one visitage web page                                                                                                                                       |
| permalink       | string    | n/a                 | hyperlink to endpoint user session details in ThousandEyes Application                                                                                                                                                                                         |
| port            | integer   | n/a                 | port used to visit target website                                                                                                                                                                                                                              |
| protocol        | string    | n/a                 | protocol used to visit target website                                                                                                                                                                                                                          |
| roundId         | integer   | n/a                 | endpoint user session round ID                                                                                                                                                                                                                                 |
| sourceAddr      | string    | n/a                 | public IP address of the endpoint agent during the session                                                                                                                                                                                                     |
| userSessionId   | string    | n/a                 | endpoint user session ID; each endpoint user session occurrence has a unique ID                                                                                                                                                                                |
| visitedSite     | string    | n/a                 | domain used to visit target website                                                                                                                                                                                                                            |

Each page object in `pages` array has following properties:

| Field           | Data Type | Units               | Notes                                                                                                                           |
| --------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| id              | string    | n/a                 | web page ID; page ID is unique only within an endpoint user session                                                             |
| title           | string    | n/a                 | web page title                                                                                                                  |
| startedDateTime | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when page load started; all dates are UTC                                                                         |
| responseCode    | integer   | n/a                 | HTTP response code                                                                                                              |
| pageTimings     | object    | n/a                 | object with two integer parameters returning the number of milliseconds to DOM Load (`onContentLoad`) and Page Load ( `onLoad`) |

`network` object has following properties:

| Field          | Data Type | Units | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------- | --------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| networkProfile | object    | n/a   | contains basic network connectivity parameters, such as IP settings, DNS settings, NIC type, WiFi settings, Proxy settings; see Example for details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| systemMetrics  | object    | n/a   | contains system metrics such as CPU and physical memory usage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| gatewayPing    | object    | n/a   | contains numeric parameters representing results of a ping test performed against the endpoint agent default gateway: `pktsSent`, `pktsReceived`, `minRtt`, `avgRtt`, `maxRtt`, `meanDevRtt`; contains only string `error` parameter if there is an error                                                                                                                                                                                                                                                                                                                                                                                   |
| ping           | object    | n/a   | contains number parameters representing results of a ping test performed against the target website: `pktsSent`, `pktsReceived`, `minRtt`, `avgRtt`, `maxRtt`, `meanDevRtt`; contains only string `error` parameter if there is an error                                                                                                                                                                                                                                                                                                                                                                                                    |
| traceroute     | object    | n/a   | contains parameters representing results of a traceroute test performed against the target website: string parameter `destination` represents target IP address, `hops` is an array of hop objects; each hop object has parameters representing hop number (integer `hop`), delay in milliseconds (integer `delay`), hop IP address (string `ipAddress`) and rDNS name (string `name`). If hop IP address is in public IP space, network string `prefix` and integer `asn` are also provided. If hop is in MPLS network, `mpls` parameter provides array of MPLS flag strings. Contains only string `error` parameter if there is an error. |
| connect        | object    | n/a   | object has one number parameter, `rtt`. `rtt` represents the number of milliseconds required to establish TCP connectivity with the target                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| icmpBlocked    | boolean   | n/a   | Set to `true` if network target is blocking ICMP echo (ping) queries                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| errors         | array     | n/a   | array of string representing possible network errors, i.e. “ping: Request timed out before getting response”                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

`systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | total physical memory of the system                                       |

`cpuUtilization` object has following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | the number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | the number of collected samples over the monitored period            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 17:12:12 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1490642120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "userSessions": [ { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "browser": { "name": "Google Chrome", "version": "57.0.2987.98" }, "committed": "2017-03-26 11:58:46", "coordinates": { "latitude": 46.0552778, "location": "Slovenia", "longitude": 14.5144444 }, "date": "2017-03-22 11:58:43", "network": { "connect": { "rtt": 77.449 }, "errors": [], "gatewayPing": { "avgRtt": 7, "maxRtt": 66, "meanDevRtt": 11, "minRtt": 0.875, "pktsReceived": 10, "pktsSent": 10 }, "icmpBlocked": false, "networkProfile": { "dnsServers": [ "8.8.8.8", "8.8.4.4" ], "gateway": "10.0.0.1", "hardwareType": "Wireless", "interfaceName": "en0", "ipAddress": "10.0.0.13", "localPrefix": "10.0.0.0", "proxyProfile": { "method": "System", "proxies": [ { "bypass": "*.local;169.254/16", "proxy": "<direct>" } ] }, "publicIpAddress": "84.255.241.1", "publicIpRange": "84.255.241.0-84.255.241.255", "subnetMask": "255.255.255.0", "type": "Ethernet", "wirelessProfile": { "bssid": "4c:ba:ba:f4:fa:fa", "channel": 1, "noise": -95, "phyMode": "802.11n", "quality": 100, "rssi": -38, "ssid": "Internet for the masses", "txRate": 130, "vendor": "Cisco" } }, "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } "ping": { "avgRtt": 24, "maxRtt": 116, "meanDevRtt": 36, "minRtt": 6.909912109375, "pktsReceived": 10, "pktsSent": 10 }, "traceroute": { "destination": "13.32.22.232", "hops": [ { "delay": 1, "hop": 1, "ipAddress": "10.0.0.1", "name": "router.local" }, { "asn": 34779, "delay": 2, "hop": 2, "ipAddress": "89.210.0.1", "name": "89-210-0-1.gw.t-2.net", "prefix": "89.210.0.0/18" }, { "asn": 34779, "delay": 2, "hop": 3, "ipAddress": "89.210.88.65", "name": "89-210-88-65.access.t-2.net", "prefix": "89.210.64.0/18" }, { "asn": 34779, "delay": 3, "hop": 4, "ipAddress": "84.255.250.46", "name": "84-255-250-46.core.t-2.net", "prefix": "84.255.192.0/18" }, { "delay": 8, "hop": 5, "ipAddress": "52.95.218.66", "name": "52.95.218.66" }, { "delay": 14, "hop": 6, "ipAddress": "52.93.38.116", "mpls": [ "L=301472,E=0,S=1,T=1" ], "name": "52.93.38.116" }, { "delay": 7, "hop": 7, "ipAddress": "52.93.38.131", "name": "52.93.38.131" }, { "delay": 7, "hop": 8, "ipAddress": "176.32.124.93", "name": "176.32.124.93" }, { "asn": 16509, "delay": 7, "hop": 12, "ipAddress": "13.32.22.232", "name": "13.32.22.232", "prefix": "13.32.20.0/22" } ] } }, "numberOfPages": 2, "orgName": "T-2 Access Network", "pages": [ { "id": "page_1", "pageTimings": { "onContentLoad": 874, "onLoad": 3492 }, "responseCode": 200, "startedDateTime": "2017-03-26 11:58:54", "title": "Network Performance Resources | ThousandEyes" }, { "id": "page_0", "pageTimings": { "onContentLoad": 1483, "onLoad": 4569 }, "responseCode": 200, "startedDateTime": "2017-03-26 11:58:43", "title": "Network Intelligence Software | ThousandEyes" } ], "permalink": "https://app.thousandeyes.com/view/endpoint-agent/?roundId=1490529480&scenarioId=sessionDetails&binSize=300000&__aid=7625", "port": 443, "protocol": "https", "roundId": 1490529480, "sourceAddr": "84.255.241.1", "userSessionId": "07625:1490529480:h3qJQTpl", "visitedSite": "www.thousandeyes.com" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET POST /v6/endpoint-data/user-sessions/web` Endpoint web pages list](broken-reference)

Returns a list of all endpoint web sessions. Sessions from the last round are provided unless an explicit start and end is provided with `from`, `to` or `window` optional parameters.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `page={pageNo}` this parameter is going to be deprecated - please rely on the URL in the `pages[next]` element included in the response. See [Pagination](https://developer.thousandeyes.com/v6/#/pagination) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Optional Filtering <a href="#optional_filtering" id="optional_filtering"></a>

`/endpoint-data` endpoints support optional filtering. See [Endpoint Data Filtering](broken-reference) for more information.

#### Request <a href="#request" id="request"></a>

* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/user-sessions/web.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object. `webSessions` parameter returns an array of web pages user loaded in an endpoint session. Pages shown are from the latest round, or based on the time range specified. Each entry represents an endpoint user session web page.

Each page object in `webSessions` array has following properties:

| Field         | Data Type | Units               | Notes                                                                                                                           |
| ------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| pageId        | string    | n/a                 | web page ID; page ID is unique only within an endpoint user session                                                             |
| pageUrl       | string    | n/a                 | web page title                                                                                                                  |
| date          | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when page load started; all dates are UTC                                                                         |
| responseCode  | integer   | n/a                 | HTTP response code                                                                                                              |
| responseTime  | integer   | n/a                 | number of milliseconds to HTTP server response                                                                                  |
| pageTimings   | object    | n/a                 | object with two integer parameters returning the number of milliseconds to DOM Load (`onContentLoad`) and Page Load ( `onLoad`) |
| agentId       | string    | n/a                 | endpoint agent ID                                                                                                               |
| userSessionId | string    | n/a                 | endpoint user session ID                                                                                                        |
| roundId       | integer   | n/a                 | endpoint user session round ID                                                                                                  |
| systemMetrics | object    | n/a                 | contains system metrics such as CPU and physical memory usage                                                                   |

`systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | total physical memory of the system                                       |

`cpuUtilization` object has following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | the number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | the number of collected samples over the monitored period            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 13:47:12 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 598 X-Organization-Rate-Limit-Reset: 1490622120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "webSessions": [ { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "date": "2017-03-22 11:58:54", "pageId": "page_1", "pageTimings": { "onContentLoad": 874, "onLoad": 3492 }, "pageTitle": "Network Performance Resources | ThousandEyes", "pageUrl": "https://www.thousandeyes.com/resources", "responseCode": 200, "responseTime": 150, "roundId": 1490529480, "userSessionId": "07625:1490529480:h3qJQTpl", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } }, { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "date": "2017-03-22 11:58:43", "pageId": "page_0", "pageTimings": { "onContentLoad": 1483, "onLoad": 4569 }, "pageTitle": "Network Intelligence Software | ThousandEyes", "pageUrl": "https://www.thousandeyes.com/", "responseCode": 200, "responseTime": 395, "roundId": 1490529480, "userSessionId": "07625:1490529480:h3qJQTpl", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } } ] "pages": { "current": 1 } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/user-sessions/{sessionId}/page/{pageId}` Endpoint web page details](broken-reference)

Returns details for endpoint user session web page request. Provides complete waterfall information with all object requests.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* {sessionId} corresponds to the id of a endpoint user sessions, see the Endpoint user session list endpoint for a listing of endpoint user sessions.
* {pageId} corresponds to the id of a web page, see the Endpoint user session details endpoint for a listing of web pages.
* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/user-sessions/07625:1490529480:h3qJQTpl/page/page_1.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed data of an endpoint user session web page request.

Returned object has one parameter: `har`. `har` is an HAR object according to the HTTP Archive 1.2 specifications. You can read more about the specification [here](http://www.softwareishard.com/blog/har-12-spec/).

In addition to standard fields, the object `har` includes a custom property `_systemMetrics` which contain metrics about CPU and physical memory usage.

`_systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | total physical memory of the system                                       |

`cpuUtilization` object has following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | the number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | the number of collected samples over the monitored period            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 17:13:02 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 598 X-Organization-Rate-Limit-Reset: 1490642120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "har": { "log": { "browser": { "name": "Google Chrome", "version": "57.0.2987.98" }, "creator": { "name": "ThousandEyes Endpoint Agent", "version": "0.47.0" }, "entries": [ { "pageref": "page_1", "request": { "headers": [ { "name": "Upgrade-Insecure-Requests", "value": "1" }, { "name": "User-Agent", "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.98 Safari/537.36" }, { "name": "Accept", "value": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8" }, { "name": "Referer", "value": "https://www.thousandeyes.com/" }, { "name": "Accept-Encoding", "value": "gzip, deflate, sdch, br" }, { "name": "Accept-Language", "value": "en-US,en;q=0.6" }, { "name": "Cookie", "value": "(removed)" } ], "method": "GET", "queryString": [], "url": "https://www.thousandeyes.com/resources" }, "response": { "bodySize": 17776, "content": { "mimeType": "text/html;charset=ISO-8859-1", "size": 17776 }, "headers": [ { "name": "Content-Type", "value": "text/html;charset=ISO-8859-1" }, { "name": "Content-Length", "value": "17776" }, { "name": "Connection", "value": "keep-alive" }, { "name": "Date", "value": "Sun, 26 Mar 2017 11:58:54 GMT" }, { "name": "Server", "value": "Apache" }, { "name": "Cache-Control", "value": "max-age=600, must-revalidate" }, { "name": "Content-Language", "value": "en-US" }, { "name": "Content-Encoding", "value": "gzip" }, { "name": "X-Frame-Options", "value": "sameorigin" }, { "name": "Strict-Transport-Security", "value": "max-age=31536000" }, { "name": "Vary", "value": "Accept-Encoding" }, { "name": "X-Cache", "value": "Miss from cloudfront" }, { "name": "Via", "value": "1.1 5dbe09af3a2c87121e31ffa67f174f66.cloudfront.net (CloudFront)" }, { "name": "X-Amz-Cf-Id", "value": "YkvlkBNKgHt5aMu9vcS22Z8kHn1MUr-8adupwhDk3j9vF-TpSyIxZA==" } ], "headersSize": 527, "redirectURL": "", "status": 200, "statusText": "OK" }, "serverIPAddress": "13.32.22.80", "startedDateTime": "2017-03-22T11:58:54.123+02:00", "time": 177, "timings": { "blocked": -1, "connect": -1, "dns": -1, "receive": 27, "send": -1, "ssl": -1, "wait": 150 } }, { "pageref": "page_1", "request": { "headers": [ { "name": "User-Agent", "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.98 Safari/537.36" }, { "name": "Accept", "value": "*/*" }, { "name": "Referer", "value": "https://www.thousandeyes.com/resources" }, { "name": "Accept-Encoding", "value": "gzip, deflate, sdch, br" }, { "name": "Accept-Language", "value": "en-US,en;q=0.6" } ], "method": "GET", "queryString": [], "url": "https://use.typekit.net/cjy5myw.js" }, "response": { "bodySize": 0, "content": { "mimeType": "text/javascript;charset=utf-8", "size": 7814 }, "headers": [ { "name": "status", "value": "200" }, { "name": "access-control-allow-origin", "value": "*" }, { "name": "cache-control", "value": "public, max-age=600, stale-while-revalidate=604800" }, { "name": "content-encoding", "value": "gzip" }, { "name": "content-type", "value": "text/javascript;charset=utf-8" }, { "name": "server", "value": "nginx" }, { "name": "status", "value": "200 OK" }, { "name": "timing-allow-origin", "value": "*" }, { "name": "vary", "value": "Accept-Encoding" }, { "name": "content-length", "value": "7814" }, { "name": "date", "value": "Sun, 26 Mar 2017 11:58:43 GMT" } ], "headersSize": 334, "redirectURL": "", "status": 200, "statusText": "OK" }, "serverIPAddress": "104.103.103.234", "startedDateTime": "2017-03-22T11:58:54.123+02:00", "time": 72, "timings": { "blocked": -1, "connect": -1, "dns": -1, "receive": 10, "send": -1, "ssl": -1, "wait": 62 } } [...] ], "pages": [ { "id": "page_1", "pageTimings": { "onContentLoad": 874, "onLoad": 3492 }, "responseCode": 200, "startedDateTime": "2017-03-22T11:58:54.123+02:00", "title": "Network Performance Resources | ThousandEyes" } ], "_systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } "version": "1.2" } } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET POST /v6/endpoint-data/user-sessions/network` Endpoint network sessions list](broken-reference)

Returns a list of all endpoint network sessions. Sessions from the last round are provided unless an explicit start and end is provided with `from`, `to` or `window` optional parameters.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `page={pageNo}` this parameter is going to be deprecated - please rely on the URL in the `pages[next]` element included in the response. See [Pagination](https://developer.thousandeyes.com/v6/#/pagination) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Optional Filtering <a href="#optional_filtering" id="optional_filtering"></a>

`/endpoint-data` endpoints support optional filtering. See [Endpoint Data Filtering](broken-reference) for more information.

#### Request <a href="#request" id="request"></a>

* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/user-sessions/network.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object. `networkSessions` parameter returns an array of endpoint network session. Network sessions shown are from the latest round, or based on the time range specified. Each entry represents an endpoint network session.

Each page object in `networkSessions` array has following properties:

| Field         | Data Type | Units               | Notes                                                                                                                                                                                                                            |
| ------------- | --------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| userSessionId | string    | n/a                 | endpoint user session ID; each endpoint user session occurrence has a unique ID                                                                                                                                                  |
| agentId       | string    | n/a                 | endpoint agent ID                                                                                                                                                                                                                |
| roundId       | integer   | n/a                 | endpoint user session round ID                                                                                                                                                                                                   |
| date          | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when endpoint user session took place; all dates are UTC                                                                                                                                                           |
| destination   | object    | n/a                 | contains number parameters representing results of a network test performed against the target website: `latency`, `loss` and `jitter`, `avgRtt`, `maxRtt`, `meanDevRtt`; string parameter `target` represents target IP address |
| systemMetrics | object    | n/a                 | contains system metrics such as CPU and physical memory usage                                                                                                                                                                    |

`systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | total physical memory of the system                                       |

`cpuUtilization` object has following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | the number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | the number of collected samples over the monitored period            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 13:47:53 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 597 X-Organization-Rate-Limit-Reset: 1490622120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "webSessions": [ "networkSessions": [ { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "date": "2017-03-22 11:58:42", "destination": { "jitter": 46, "latency": 150, "loss": 0.0, "target": "54.208.6.220" }, "roundId": 1490529480, "userSessionId": "07625:1490529480:aVDViw0i", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } }, { "agentId": "3fde6422-f119-40e1-ae32-d08a1243c038", "date": "2017-03-22 11:58:43", "destination": { "jitter": 36, "latency": 24, "loss": 0.0, "target": "13.32.22.232" }, "roundId": 1490529480, "userSessionId": "07625:1490529480:h3qJQTpl", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } } ] "pages": { "current": 1 } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET POST /v6/endpoint-data/network-topology` Endpoint network topology list](broken-reference)

Returns a list of all endpoint network topology results. Results from the last round are provided unless an explicit start and end is provided with `from`, `to` or `window` optional parameters.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `page={pageNo}` this parameter is going to be deprecated - please rely on the URL in the `pages[next]` element included in the response. See [Pagination](https://developer.thousandeyes.com/v6/#/pagination) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Warning <a href="#warning" id="warning"></a>

Note that a maximum of 12h worth of data can be retreived at once. If you need more, you need to make multiple requests.

#### Optional Filtering <a href="#optional_filtering" id="optional_filtering"></a>

`/endpoint-data` endpoints support optional filtering. See [Endpoint Data Filtering](broken-reference) for more information.

#### Request <a href="#request" id="request"></a>

* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/network-topology.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object. `networkProbes` parameter returns an array of network topology probes. Network topology probes shown are from the latest round, or based on the time range specified. Each entry represents a network topology probe.

Each object in `networkProbes` array has following properties:

| Field          | Data Type | Units               | Notes                                                                                                                                                                  |
| -------------- | --------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| networkProbeId | string    | n/a                 | network probe ID; each network probe occurrence has a unique ID                                                                                                        |
| agentId        | string    | n/a                 | endpoint agent ID                                                                                                                                                      |
| roundId        | integer   | n/a                 | endpoint user session round ID                                                                                                                                         |
| date           | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when network probe took place; all dates are UTC                                                                                                         |
| target         | string    | n/a                 | IP of the target the network probe was performed against; this is typically a default gateway, proxy or VPN endpoint                                                   |
| icmpPing       | object    | n/a                 | contains number parameters representing results of a ping test performed against the target: `pktsSent`, `pktsReceived`, `minRtt`, `avgRtt`, `maxRtt` and `meanDevRtt` |
| icmpBlocked    | boolean   | n/a                 | true when network path trace could not complete, but TCP connection to the target was successfully established                                                         |
| systemMetrics  | object    | n/a                 | contains system metrics such as CPU and physical memory usage                                                                                                          |

`systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | total physical memory of the system                                       |

`cpuUtilization` object has following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | the number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | the number of collected samples over the monitored period            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 13:48:23 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 596 X-Organization-Rate-Limit-Reset: 1490622120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "networkProbes": [ { "agentId": "c7a58c49-4d1a-481f-b41c-0e72ea4b9239", "date": "2017-03-26 13:55:01", "icmpPing": { "avgRtt": 0, "maxRtt": 0, "meanDevRtt": 0, "minRtt": 0.0, "pktsReceived": 10, "pktsSent": 10 }, "networkProbeId": "00160:54c3a4b180c6:1490536500:c7a58c49", "roundId": 1490536500, "target": "10.0.2.2", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } }, { "agentId": "c7a58c49-4d1a-481f-b41c-0e72ea4b9239", "date": "2017-03-26 14:02:00", "icmpPing": { "avgRtt": 0, "maxRtt": 0, "meanDevRtt": 0, "minRtt": 0.0, "pktsReceived": 10, "pktsSent": 10 }, "networkProbeId": "00160:54c3a4b180c6:1490536800:c7a58c49", "roundId": 1490536800, "target": "10.0.2.2", "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } } ] "pages": { "current": 1 } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-data/network-topology/{networkProbeId}` Endpoint network topology details](broken-reference)

Returns details for a network topology probe

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* {networkProbeId} corresponds to the id of a network probe, see the Endpoint network topology list endpoint for a listing of network probes.
* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/network-topology/00160:39c518560de9:1491651900:236e6f18.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed data of a network topology probe.

| Field          | Data Type | Units               | Notes                                                                                                                                                                                                                                                   |
| -------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| networkProbeId | string    | n/a                 | network probe ID; each network probe occurrence has a unique ID                                                                                                                                                                                         |
| agentId        | string    | n/a                 | endpoint agent ID                                                                                                                                                                                                                                       |
| roundId        | integer   | n/a                 | endpoint user session round ID                                                                                                                                                                                                                          |
| date           | dateTime  | yyyy-MM-dd hh:mm:ss | the date/time when network probe took place; all dates are UTC                                                                                                                                                                                          |
| target         | string    | n/a                 | IP of the target the network probe was performed against; this is typically a default gateway, proxy or VPN endpoint                                                                                                                                    |
| coordinates    | object    | n/a                 | object contains approximate GPS location of the endpoint agent, based on endpoint agent’s public IP address; `latitude` and `longitude` are numeric representations of GPS coordinates, `location` is a string representing named geographical location |
| icmpPing       | object    | n/a                 | contains number parameters representing results of a ping test performed against the target: `pktsSent`, `pktsReceived`, `minRtt`, `avgRtt`, `maxRtt` and `meanDevRtt`                                                                                  |
| networkProfile | object    | n/a                 | contains basic network connectivity parameters, such as IP settings, DNS settings, NIC type, WiFi settings, Proxy settings; see Example for details                                                                                                     |
| systemMetrics  | object    | n/a                 | contains system metrics such as CPU and physical memory usage                                                                                                                                                                                           |

`systemMetrics` object has following properties:

| Field                    | Data Type | Units        | Notes                                                                     |
| ------------------------ | --------- | ------------ | ------------------------------------------------------------------------- |
| startTimeMs              | integer   | milliseconds | time at which metrics collection started, as milliseconds since the Epoch |
| endTimeMs                | integer   | milliseconds | time at which metrics collection ended, as milliseconds since the Epoch   |
| cpuUtilization           | object    | n/a          | contains utilization of the system’s processors over the monitored period |
| physicalMemoryUsedBytes  | object    | n/a          | contains metrics about used physical memory                               |
| physicalMemoryTotalBytes | integer   | bytes        | total physical memory of the system                                       |

`cpuUtilization` object has following properties:

| Field  | Data Type | Units      | Notes                                                                                      |
| ------ | --------- | ---------- | ------------------------------------------------------------------------------------------ |
| min    | double    | \[0.0-1.0] | minimal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| max    | double    | \[0.0-1.0] | maximal value of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period      |
| mean   | double    | \[0.0-1.0] | mean of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period               |
| median | double    | \[0.0-1.0] | median of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period             |
| stdDev | double    | \[0.0-1.0] | standard deviation of CPU usage sampled (in range of \[0.0-1.0]) over the monitored period |
| count  | integer   | n/a        | the number of collected samples over the monitored period                                  |

`physicalMemoryUsedBytes` object has following properties:

| Field  | Data Type | Units | Notes                                                                |
| ------ | --------- | ----- | -------------------------------------------------------------------- |
| min    | double    | bytes | minimal value of memory usage sampled over the monitored period      |
| max    | double    | bytes | maximal value of memory usage sampled over the monitored period      |
| mean   | double    | bytes | mean value of memory usage sampled over the monitored period         |
| median | double    | bytes | median value of memory usage sampled over the monitored period       |
| stdDev | double    | bytes | standard deviation of memory usage sampled over the monitored period |
| count  | integer   | n/a   | the number of collected samples over the monitored period            |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 22 Mar 2017 18:03:02 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1490642120 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "networkProbes": [ { "agentId": "236e6f18-9637-4a2f-b15f-7aa6a29c9fce", "coordinates": { "latitude": 46.0552778, "location": "Slovenia", "longitude": 14.5144444 }, "date": "2017-03-21 11:49:35", "icmpPing": { "avgRtt": 5, "maxRtt": 26, "meanDevRtt": 6, "minRtt": 0.9130859375, "pktsReceived": 9, "pktsSent": 10 }, "networkProbeId": "00160:39c518560de9:1491651900:236e6f18", "networkProfile": { "dnsServers": [ "10.20.10.1" ], "gateway": "10.20.10.1", "hardwareType": "Wireless", "interfaceName": "en0", "ipAddress": "10.20.10.13", "localPrefix": "10.20.10.0", "publicIpAddress": "84.255.241.1", "publicIpRange": "84.255.241.0-84.255.241.255", "subnetMask": "255.255.255.0", "type": "Ethernet", "wirelessProfile": { "bssid": "4c:ba:ba:f4:fa:fa", "channel": 11, "noise": -98, "phyMode": "802.11n", "quality": 84, "rssi": -58, "ssid": "Internet for the masses", "txRate": 130, "vendor": "Cisco" } }, "systemMetrics": { "startTimeMs": 1581508857327, "endTimeMs": 1581508867333, "cpuUtilization": { "min": 0.30859375, "max": 0.5625, "mean": 0.38931831001805056, "median": 0.353515625, "stdDev": 0.08389194281742307, "count": 10 }, "physicalMemoryUsedBytes": { "min": 1.2805128192E10, "max": 1.2825530368E10, "mean": 1.281914582109091E10, "median": 1.2818219008E10, "stdDev": 5741124.05691331, "count": 11 }, "physicalMemoryTotalBytes": 17069891584 } "roundId": 1491651900, "target": "10.20.10.1" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[Endpoint data filtering](broken-reference)

`/endpoint-data` API endpoints support optional filtering. Results from the following API endpoints:

* `/endpoint-data/user-sessions`
* `/endpoint-data/user-sessions/web`
* `/endpoint-data/user-sessions/network`
* `/endpoint-data/network-topology`

can be filtered by providing additional filters in form of POST JSON object.

### Request <a href="#request" id="request"></a>

Standard request to the endpoints supporting filtering is performed using the GET method. In order to apply filtering, request has to be done with POST method.

#### Post Data <a href="#post_data" id="post_data"></a>

When POSTing data to the endpoints, users can use provide filters as a JSON object containing `searchFilters` parameter. `searchFilters` is an array of searchFilter objects. Each searchFilter object must have the following parameters:

| Field  | Data Type | Notes                    |
| ------ | --------- | ------------------------ |
| key    | string    | parameter to be filtered |
| values | array     | an array                 |

When multiple searchFilter objects are provider, a logical AND is applied between the filters.

When a searchFilter contains multiple `values`, a logical OR is applies between the filters

Search filter key can be any of the following:

| Key           | API endpoint      | Notes                                                                        |
| ------------- | ----------------- | ---------------------------------------------------------------------------- |
| location      | all               | location of the endpoint agent, i.e. `San Francisco Bay Area` or `Germany`   |
| connection    | all               | network connection type; `Ethernet`, `Loopback` or `Wireless`                |
| trigger       | all               | user session trigger; `auto` or `user`                                       |
| platform      | all               | endpoint agent platform OS; `Mac` or `Windows`                               |
| gateway       | all               | endpoint agent default gateway IP address                                    |
| proxyTarget   | all               | endpoint agent proxy IP address                                              |
| vpnTarget     | all               | endpoint agent VPN endpoint IP address                                       |
| agentId       | all               | endpoind agent ID, i.e. `3fde6422-f119-40e1-ae32-d08a1243c038`               |
| networkId     | all               | network ID, i.e. `660b34109d12`                                              |
| ssid          | all               | WiFi SSID                                                                    |
| bssid         | all               | WiFi BSSID                                                                   |
| domain        | /user-sessions    | web site **base** domain visited during the session, i.e. `thousandeyes.com` |
| visitedSite   | /user-sessions    | web site domain visited during the session, i.e. `app.thousandeyes.com`      |
| destinationIp | /user-sessions    | web site destination IP address                                              |
| type          | /network-topology | network topology type; `vpn`, `proxy` or `gateway`                           |

#### Example <a href="#example" id="example"></a>

Return all endpoint user sessions between 2017-04-08 00:00:00 and 20:00:00 UTC, performed from user agents on a WiFi connection AND visiting any sites from thousandeyes.com OR salesforce.com domains:

`$ curl https://api.thousandeyes.com/v6/endpoint-data/user-sessions.json?from=2017-04-08T00:00:00\&to=2017-04-08T20:00:00 \ -d '{ "searchFilters": [ { "key": "connection", "values": ["Wireless"] }, { "key": "domain", "values": ["thousandeyes.com","salesforce.com"] } ] }' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns normal response, as documented by each API endpoint. If filter conditions match no objects in a given time period, returned main object array has no children elements.

`HTTP/1.1 200 OK Server: nginx Date: Sun, 09 Apr 2017 10:00:04 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 600 X-Organization-Rate-Limit-Remaining: 599 X-Organization-Rate-Limit-Reset: 1491732060 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "from": "2017-04-08 00:00:00", "pages": { "current": 1 }, "to": "2017-04-08 20:00:00", "userSessions": [ { "agentId": "236e6f18-9637-4a2f-b15f-7aa6a29c9fce", "committed": "2017-04-08 11:49:38", "date": "2017-04-08 11:49:36", "numberOfPages": 3, "orgName": "Happy Network Services", "permalink": "https://app.thousandeyes.com/view/endpoint-agent/?roundId=1491652140&scenarioId=sessionDetails&binSize=300000&__aid=160", "port": 443, "protocol": "https", "roundId": 1491652140, "sourceAddr": "78.153.54.206", "userSessionId": "00160:1491652140:EDG4jXHI", "visitedSite": "success.thousandeyes.com" }, { "agentId": "236e6f18-9637-4a2f-b15f-7aa6a29c9fce", "committed": "2017-04-08 11:53:29", "date": "2017-04-08 11:53:28", "numberOfPages": 1, "orgName": "Happy Network Services", "permalink": "https://app.thousandeyes.com/view/endpoint-agent/?roundId=1491652380&scenarioId=sessionDetails&binSize=300000&__aid=160", "port": 443, "protocol": "https", "roundId": 1491652380, "sourceAddr": "78.153.54.206", "userSessionId": "00160:1491652380:CEwYgJIF", "visitedSite": "app.thousandeyes.com" } ] }`

[`GET /v6/endpoint-data/networks` Endpoint networks](broken-reference)

Returns a list of all the networks from which endpoint agents performed user sessions.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

**Example**

`$ curl https://api.thousandeyes.com/v6/endpoint-data/networks.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an object. `privateNetworks` parameter returns an array of networks.

Each network object in `privateNetworks` array has following properties:

| Field         | Data Type | Units | Notes                                               |
| ------------- | --------- | ----- | --------------------------------------------------- |
| networkId     | string    | n/a   | network ID; each network occurrence has a unique ID |
| networkName   | string    | n/a   | network name                                        |
| localPrefix   | string    | n/a   | local private address of the network                |
| publicIpRange | string    | n/a   | public IP range of the network                      |

`HTTP/1.1 200 OK Server: nginx Date: Sun, 09 Apr 2017 11:15:32 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1491736560 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-4`

**Body**

`{ "privateNetworks": [ { "networkId": "006c4fa7a054", "localPrefix": "10.5.51.0", "networkName": "10.5.51.0 (in 178.216.56.0/21)", "publicIpRange": "178.216.56.0-178.216.63.255" }, { "networkId": "06e8270d2582", "localPrefix": "172.22.2.0", "networkName": "172.22.2.0 (in 188.230.129.0/24)", "publicIpRange": "188.230.129.0-188.230.129.255" } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
