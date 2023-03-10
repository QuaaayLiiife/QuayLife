# TEST DATA

[`GET /v7/net/path-vis/{testId}` (Network) Path visualization](broken-reference)

Returns a hop-by-hop summary of the path trace data collected during path visualization. In each path visualization attempt, three attempts are made to reach the destination, and the entire path will be shown in sequence. For agent-to-agent tests, there’s a special case to consider, since the test can be bidirectional. A **time frame** must be specified, or the current round of data will be returned.

Consider agents A, B and C testing agent D, on a bidirectional basis. To query for the route from agent A to agent D, query with testId?direction=TO\_TARGET. For the path from D to A, query with testId?direction=FROM\_TARGET. To get both paths, query without the direction parameter. In all cases, the source field will reflect agent A, and the destination field will reflect agent D, but the direction field will show the direction of the trace.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v7/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v7/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v7/#/timeranges) for more information.
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information
* `direction=[FROM_TARGET, TO_TARGET]` Applicable only for bidirectional Agent-to-Agent tests, specifies the direction for the metrics being retrieved. If available, bidirectional data is returned by default.

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the test you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field                   | Data Type | Units        | Notes                                                                       |
| ----------------------- | --------- | ------------ | --------------------------------------------------------------------------- |
| agentId                 | integer   | n/a          | unique ID of agent, from `/agents` endpoint                                 |
| agentName               | string    | n/a          | display name of the agent responding                                        |
| countryId               | string    | n/a          | ISO-3166-1 alpha-2 country code of the agent                                |
| date                    | dateTime  | n/a          | yyyy-MM-dd hh:mm:ss, in UTC                                                 |
| roundId                 | long      | seconds      | epoch time (seconds) indicating the start time of the round                 |
| permalink               | url       | n/a          | link to jump to this result in the front end                                |
| server                  | url       | n/a          | target server, including port (if method used is TCP)                       |
| serverIp                | string    | n/a          | ip address of target server                                                 |
| sourceIp                | string    | n/a          | ip address of source agent                                                  |
| sourcePrefix            | string    | n/a          | ip prefix of source agent                                                   |
| routes                  | array     | n/a          | shows 3 iterations of path trace, with each iteration specified by a pathId |
| routes.pathId           | string    | n/a          | unique ID of path trace                                                     |
| routes.hops             | array     | n/a          | array of hop objects indicating each step in the traceroute                 |
| routes.hops.hop         | integer   | n/a          | index of hop                                                                |
| routes.hops.ipAddress   | string    | n/a          | IP address of the hop                                                       |
| routes.hop.prefix       | string    | n/a          | Prefix of IP address shown in CIDR                                          |
| routes.hop.rdns         | string    | n/a          | reverse DNS entry of IP, if available                                       |
| routes.hop.network      | string    | n/a          | Autonomous System originating the prefix                                    |
| routes.hop.responseTime | integer   | milliseconds | RTT to the hop’s IP                                                         |
| routes.hop.location     | string    | n/a          | location information for the hop                                            |
| routes.hop.mpls         | string    | n/a          | Multiprotocol Label Switching information, if available                     |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/net/path-vis/1035482.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Mon, 03 Feb 2020 22:28:32 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: 6znrq Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 235 X-Organization-Rate-Limit-Reset: 1580768940 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "net": { "test": { "enabled": 1, "testId": 817, "testName": "http://www.thousandeyes.com", "type": "http-server", "interval": 900, "url": "http://www.thousandeyes.com", "modifiedDate": "2013-05-11 02:02:21", "networkMeasurements": 1, "createdBy": "API Sandbox User (noreply@thousandeyes.com)", "modifiedBy": "API Sandbox User (noreply@thousandeyes.com)", "createdDate": "2012-06-28 19:33:12", "apiLinks": [...] }, "pathVis": [ { "server": "www.google.com:443", "serverIp": "172.217.170.68", "sourceIp": "196.40.106.237", "sourcePrefix": "196.40.96.0/20", "agentName": "Cape Town, South Africa", "countryId": "ZA", "date": "2020-02-03 22:33:01", "agentId": 25, "roundId": 1580769180, "routes": [ { "pathId": "4711301366345855606023718047703941305741293841502186803", "hops": [ { "hop": 2, "ipAddress": "41.204.206.37", "prefix": "41.204.192.0/20", "rdns": "core-router1.cpt2.host-h.net", "responseTime": 0, "location": "Cape Town, South Africa", "network": "HETZNER (Pty) Ltd (AS 37153)" }, { "hop": 3, "ipAddress": "41.66.133.1", "prefix": "41.66.128.0/18", "rdns": "41-66-133-1-2.WC-RO-HET-MEE-1AE-0-4007.africainx.net", "responseTime": 0, "location": "Cape Town, South Africa", "network": "AFRICAINX (AS 37179)" }, ... ] }, { "pathId": "4711301366345855606023718047703941305741293841502186801", "hops": [ { "hop": 2, "ipAddress": "41.204.206.37", "prefix": "41.204.192.0/20", "rdns": "core-router1.cpt2.host-h.net", "responseTime": 0, "location": "Cape Town, South Africa", "network": "HETZNER (Pty) Ltd (AS 37153)" }, { "hop": 3, "ipAddress": "41.66.133.1", "prefix": "41.66.128.0/18", "rdns": "41-66-133-1-2.WC-RO-HET-MEE-1AE-0-4007.africainx.net", "responseTime": 0, "location": "Cape Town, South Africa", "network": "AFRICAINX (AS 37179)" }, ... ] } ], "permalink": "https://app.thousandeyes.com/net/path-vis?__a=154608&testId=1035482&roundId=1580769180&serverId=2696&agentId=25" }, ... ] "pages": { "current": 1 } } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).
