# Instant tests

[`POST /v6/instant/{testType}` Instant test](broken-reference)

Creates and runs a new Instant test in ThousandEyes, based on properties provided in the POST data. In order to create and run an Instant test, the user attempting the creation must be a Regular user or have the following permissions:

* API Access
* View tests

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

*   `{testType}` corresponds to any of the following options:

    * agent-to-agent
    * agent-to-server
    * http-server
    * page-load
    * transactions
    * web-transactions
    * ftp-server
    * dns-trace
    * dns-server
    * dns-dnssec
    * sip-server
    * voice (RTP Stream)

    _Note: bgp tests are currently not supported_
* Request body should contain fields to be set during creation. See the [Test Metadata](https://developer.thousandeyes.com/v6/tests/#/test\_metadata) page for fields available during test creation. The following fields are accepted but will be ignored by the Instant test API:
  * interval
  * subinterval
  * alertsEnabled
  * alertRules
  * bgpMeasurements
  * bgpMonitors

#### Response <a href="#response" id="response"></a>

If an instant test is successfully created and ran, an HTTP/201 CREATED response will be returned, and the test definition will be returned. See the example below.

Response does not include instant test results. Once the instant test is created and ran, results can be retrieved using [Test Data](https://developer.thousandeyes.com/v6/test\_data) endpoints. API test data endpoints URLs are provided in test definition output upon instant test creation. See the example below.

#### Example <a href="#example" id="example"></a>

Please note, Instant tests are not allowed on the Sandbox API account, and will not work if attempted. The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/instant/agent-to-server \ -d '{ "agents": [ {"agentId": 113} ], "testName": "API Instant test", "server": "www.thousandeyes.com" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 201 Created Server: nginx Date: Tue, 14 Mar 2017 16:21:58 GMT Content-Type: application/json Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1489508520 X-Instant-Test-Rate-Limit-Limit: 97 X-Instant-Test-Rate-Limit-Remaining: 95 X-Instant-Test-Rate-Limit-Reset: 1489508520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-4`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

**Body**

`{ "test": [ { "agents": [ { "agentId": 113, "agentName": "Test Agent", "agentType": "Enterprise Cluster", "countryId": "DE", "ipAddresses": [ "10.0.0.1" ], "location": "Germany", "network": "Hetzner Online GmbH (AS 24940)", "prefix": "136.243.0.0/16", "publicIpAddresses": [ "136.243.0.1" ] } ], "alertsEnabled": 0, "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/tests/344811", "rel": "self" }, { "href": "https://api.thousandeyes.com/v6/net/metrics/344811", "rel": "data" }, { "href": "https://api.thousandeyes.com/v6/net/path-vis/344811", "rel": "data" } ], "bandwidthMeasurements": 0, "bgpMeasurements": 0, "createdBy": "ThousandEyes (noreply@thousandeyes.com)", "createdDate": "2017-03-14 16:21:58", "enabled": 1, "interval": 0, "liveShare": 0, "mtuMeasurements": 1, "networkMeasurements": 1, "pingPayloadSize": -1, "protocol": "TCP", "savedEvent": 0, "server": "www.thousandeyes.com:80", "testId": 344811, "testName": "API Instant test", "type": "agent-to-server" } ] }`

[`POST /v6/instant/{testId}/rerun` Instant test rerun](broken-reference)

Reruns an existent Instant test in ThousandEyes. In order to rerun an Instant test, the user attempting the rerun must be a Regular user or have the following permissions:

* API Access
* View tests

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{testId}` the ID of the Instant test you wish to rerun.
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

There is no response body for this request. See the example below.

Once the instant test is reran, results can be retrieved using [Test Data](https://developer.thousandeyes.com/v6/test\_data) endpoints.

#### Example <a href="#example" id="example"></a>

Please note, Instant tests are not allowed on the Sandbox API account, and will not work if attempted. The following example is presented for documentation and reference purposes only.

`$curl -X POST -i https://api.thousandeyes.com/v6/instant/344811/rerun \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Tue, 14 Mar 2017 18:10:22 GMT Content-Length: 0 Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1489515060 X-Instant-Test-Rate-Limit-Limit: 97 X-Instant-Test-Rate-Limit-Remaining: 96 X-Instant-Test-Rate-Limit-Reset: 1489515060 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
