# ThousandEyes Developer Reference v6

### Overview

[Welcome](broken-reference)

Most applications will use an existing wrapper library in the language of your choice. Over the past several months, we’ve had discussions with customers using LINQ, Microsoft .NET, Python and Java to access our API content.

That said, it’s important to get familiar with the underlying methods used in the API before getting your hands dirty.

For simplicity’s sake, we’ll use cURL for documenting examples, and outputs will be shown in JSON (because it’s less verbose than XML and lends itself more readily to readability) - see [response formats](broken-reference) for more detailed information on controlling output format.

Let’s start by accessing an information-only API endpoint.

`$ curl https://api.thousandeyes.com/v6/status.json`

**Output**

This returns the current controller time (in epoch format), if run correctly. This is simply intended for verification that the API is currently running.

`{"timestamp":1492606869263}`

Let’s show the response headers, using the -i flag:

`$ curl -i https://api.thousandeyes.com/v6/status.json`

**Output**

Most of the headers are inconsequential - you’ll see the server’s date and time, version, http status code for your request. When working with our API programmatically, always check to make sure you receive an HTTP/200 response code to your request.

`HTTP/1.1 200 OK Server: nginx Date: Wed, 19 Apr 2017 13:01:09 GMT Content-Type: text/xml Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-5`

`{"timestamp":1492606869263}`

For information on our HTTP status responses, see the [response status codes documentation](broken-reference).

[Authentication](broken-reference)

The ThousandEyes API accepts Basic HTTP or OAuth bearer token as authentication methods, however in the EU region only the OAuth Bearer token is supported. This is specified using the HTTP request wrapper of your choice. Both the Basic Authentication Token and the OAuth Bearer Token referenced here and throughout the developer reference are available from your [Account Settings > Users and Roles page](https://app.thousandeyes.com/account-settings/users-roles/?section=profile) under the “Profile” tab, in the “User API Tokens” section.

The example below shows a standard request using cURL with basic authentication:

`$ curl -i https://api.thousandeyes.com/v6/status \ -u {email}:{authToken}`

The following example leverages cURL presenting a bearer token:

`$ curl -i https://api.thousandeyes.com/v6/tests.json \ --header "Authorization: Bearer {bearerToken}"`

For basic authentication, the parameters can be provided programmatically using whichever HTTP request object is being used (most all support Basic HTTP authentication), or prepended to the target URL, in the following format:

`https://{email}:{authToken}@api.thousandeyes.com/v6/`

When providing the email address prepended to the URL, it must be URL-encoded to allow the request to proceed correctly. The `@` symbol corresponds to `%40`. See [UrlEncoding characters](https://www.w3schools.com/tags/ref\_urlencode.asp) for more information on properly formatting character strings. When using cURL, using the `-u user:token` method is strongly recommended.

For bearer token authentication, the parameter can only be read in the header in the form `Authorization: Bearer <token string>`

### Powershell Syntax <a href="#powershell_syntax" id="powershell_syntax"></a>

We’ve been asked by a number of people how to effectively create and leverage credentials against the API in Windows Powershell. Effectively, base64 encoding the email:authtoken and setting an Authorization header will allow this to be done. The following example takes two inputs and sets the required headers to work with the ThousandEyes API using basic authentication:

`[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 $apiuser = "{email}" $apipassword = "{authToken}" $authorization = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($apiuser + ":" + $apipassword)) $headers = @{"accept"= "application/json"; "content-type"= "application/json"; "authorization"= "Basic " + $authorization} $response = Invoke-WebRequest https://api.thousandeyes.com/v6/agents.json -Headers $headers $response.content`

When leveraging the bearer token, the token itself can be passed directly as a string:

`[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 $apitoken = "{bearerToken}" $headers = @{"accept"= "application/json"; "content-type"= "application/json"; "authorization"= "Bearer " + $apitoken} $response = Invoke-WebRequest https://api.thousandeyes.com//v6/tests.json -Headers $headers $response.content`

NOTE: Both the Basic Authentication Token and the OAuth Bearer Token are available from your [account settings page](https://app.thousandeyes.com/account-settings/users-roles/?section=profile) under the “Profile” tab, in the “User API Tokens” section.

### Account Lockout <a href="#account_lockout" id="account_lockout"></a>

Your account could be locked up due to a number of failed authentication attempts into the ThousandEyes application.

If attempts to reach the API are returning an `401 UNAUTHORIZED` response code, but your credentials are correct, it is possible that your account is locked up. Try logging into the App, if your account is locked up, you will be required to reset your password.

### Source IP block <a href="#source_ip_block" id="source_ip_block"></a>

When 120 or more unauthorized requests (resulting in the `401 UNAUTHORIZED` response) are issued from a given source IP address within an hour, API server will start responding with the `429 TOO MANY REQUESTS` response code. Your API script should handle `401 UNAUTHORIZED` error and prevent further requests to avoid the source IP block.

For error responses, see the [response status codes documentation](broken-reference).

[`GET /v6/account-groups` Account group context](broken-reference)

Users assigned to multiple account groups can change account group context by using the `aid={aid}` parameter. A list of account group IDs can be found using the [Account group list](http://developer.thousandeyes.com/v6/admin/#/accountgroup\_list) endpoint.

[Response formats](broken-reference)

Current version of the ThousandEyes API allows output in the following formats:

* JSON (JavaScript Object Notation)
* XML (Extensible Markup Language) [Schema document can be downloaded here](https://api.thousandeyes.com/v6/docs/te-api-v6.xsd)

It is possible to control the output of the API’s results using the following options, in descending order of precedence.

In the event that multiple, conflicting formats are specified, the order of precedence is:

1. Request
2. Accept Header
3. Querystring Parameter.

#### Append format to request <a href="#append_format_to_request" id="append_format_to_request"></a>

Appending either .xml or .json to the request will return the response in that type.

* to request a JSON response:

`$ curl https://api.thousandeyes.com/v6/tests.json \ -u {email}:{authToken}`

* to request an XML response:

`$ curl https://api.thousandeyes.com/v6/tests.xml \ -u {email}:{authToken}`

Modifying the header to accept different response types is the approach which will be most effective for guaranteeing the response type.

* `Accept:application/json` will return the response in JSON
* `Accept:text/xml` will return the response in XML

`$ curl -H "Accept: application/json" https://api.thousandeyes.com/v6/tests \ -u {email}:{authToken}`

#### QueryString Parameter <a href="#querystring_parameter" id="querystring_parameter"></a>

Appending a `format` parameter to the end of a QueryString will change the response format. The parameter and values must be in lowercase. Acceptable options:

* format=xml
* format=json

`$ curl https://api.thousandeyes.com/v6/tests?format=json \ -u {email}:{authToken}`

[Time ranges](broken-reference)

Most requests (check _Optional Parameters_ section in each endpoint), allow a time range to be specified using parameters. Specifically, `window` is allowed for alert listings, and either `window`, `from`, or `from` and `to` are allowed on all data requests. If the endpoint doesn’t respect the optional parameters, they will be ignored.

`window=[0-9]+[smhdw]?` The `window` parameter is used to specify an amount of time in the past for which to fetch data. That is, data will be retrieved from the specified amount of time ago up until the time of the request. A time window is a number followed by an optional time interval type. The supported time interval types are `s` for seconds, `m` for minutes, `h` for hours, `d` for days, and `w` for weeks. If no time interval type is specified, seconds are assumed. For example, `window=10d` would retrieve data from the last 10 days, `window=12h` would retrieve data from the last 12 hours, and `window=1200` will retrieve data from the last 1200 seconds.

`from=YYYY-mm-ddTHH:MM:SS from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS`

The `from` and `to` parameters are used to specify a specific date and time range for the data. The `to` parameter is optional – if omitted, the current time (at the time of the request) will be assumed. Dates must be specified in the ISO 8601 date-time format, with hyphens between date fields and colons between time fields. The full time (hours, minutes, and seconds) must be included. The date and time can be separated by either a space or the letter T. Example: `2012-01-01T00:00:00.` The date range is inclusive. Time zone is UTC.

Note: The `from`/`to` and `window` parameters are mutually exclusive – the server will produce a 400 error if both `window` and either `from` or `to` is specified. It will also produce a 400 error if `to` is specified without `from`.

On endpoints where `roundId` is required component of the URL, roundId is represented as epoch time corresponding to the start of a round, in seconds. For example, if a round starts on 2015-06-30 16:00:00 UTC, the roundId would be 1435680000. roundId values are always exactly divisible by the test frequency, which is specified in seconds. The next rounds for a test with a 5-minute interval would be 1435680000 + 300, or 1435680300, 1435680600, 1435680900 and so on.

For error responses, see the [response status codes documentation](broken-reference).

[Response status codes](broken-reference)

The following response status codes will be used for various endpoints around the ThousandEyes API.

| Status Code | Definition             | When you’ll see it                                                                                           |
| ----------- | ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| 200         | OK                     | Nearly every response                                                                                        |
| 201         | CREATED                | Using a `/new` endpoint (e.g. `/tests/{testType}/new`)                                                       |
| 204         | NO CONTENT             | Using a `/delete` endpoint (e.g. `/tests/{testType}/{testId}/delete`)                                        |
| 301         | MOVED PERMANENTLY      | Requests accessing a nonexistent version of the API                                                          |
| 400         | BAD REQUEST            | Malformatted requests                                                                                        |
| 401         | UNAUTHORIZED           | Invalid credentials provided or account is locked                                                            |
| 403         | FORBIDDEN              | Insufficient permissions to execute request (ie, any POST method as a regular user)                          |
| 404         | NOT FOUND              | Attempting to access an endpoint that does not exist                                                         |
| 405         | METHOD NOT ALLOWED     | Wrong request type for target endpoint (ie, POSTing data to a GET endpoint)                                  |
| 406         | NOT ACCEPTABLE         | Can be returned when the Content Type of the data returned does not match the Accept header of the request   |
| 415         | UNSUPPORTED MEDIA TYPE | Attempting to POST data in incorrect format                                                                  |
| 429         | TOO MANY REQUESTS      | You have exceeded the max number of requests per 1-minute period                                             |
| 500         | INTERNAL SERVER ERROR  | Contact [support](mailto:support@thousandeyes.com?subject=500%20Error%20on%20API) if you see this error type |
| 503         | SERVICE UNAVAILABLE    | The ThousandEyes API is currently in maintenance mode.                                                       |

[Rate limits](broken-reference)

The ThousandEyes API throttles API requests using a 240 request per minute (per organization) limit. The limit rolls over one minute from the first request in a batch, and starts again when the minute rolls over. These values are subject to change, as we work through identifying appropriate use patterns for our API.

Users can watch three header values in responses from the ThousandEyes API for information on rate limits:

`HTTP/1.1 200 OK X-Organization-Rate-Limit-Limit: 20 X-Organization-Rate-Limit-Remaining: 19 X-Organization-Rate-Limit-Reset: 1469560440`

* X-Organization-Rate-Limit-Limit is the number of requests allowed for your organization in a 60-second period.
* X-Organization-Rate-Limit-Remaining is the number of requests remaining in the current 60-second period.
* X-Organization-Rate-Limit-Reset is the UTC timestamp of the next rate limit rollover.

Instant tests are governed through a separate set of throttling controls, and allow up to 24 calls per minute. Instant test rate limit headers can be found below:

`X-Instant-Test-Rate-Limit-Limit: 2 X-Instant-Test-Rate-Limit-Remaining: 1 X-Instant-Test-Rate-Limit-Reset: 1469560440`

As above:

* X-Instant-Test-Rate-Limit-Limit is the number of requests allowed for your organization in a 60-second period.
* X-Instant-Test-Rate-Limit-Remaining is the number of requests remaining in the current 60-second period.
* X-Instant-Test-Rate-Limit-Reset: is the UTC timestamp of the next rate limit rollover.

If you are receiving an HTTP/429 (Too many requests) response code, your request was refused on the basis of a rate limit. Wait until either X-Organization-Rate-Limit-Reset value or the X-Instant-Test-Rate-Limit-Reset value (as appliable based on the type of request you are submitting) before submitting another request.

For error responses, see the [response status codes documentation](broken-reference).

[Pagination](broken-reference)

The ThousandEyes API returns data in paginated format, where the response exceeds a page of data. For requests showing current values, or less than a page worth of data, all data will be presented in a single page.

Look for the `pages` element in your response to find links to subsequent pages of result data. The `pages[next]` element will contain the URL to the next page of data. Note that where relative windows are requested, our API translates these windows into exact times, since it may take time to iterate through several pages of response data.

* if `pages[next]` is present, there is more data available. If not, you are on the last page of data.

A sample of a response including pages is shown below:

**Request**

`$ curl -i https://api.thousandeyes.com/v6/web/page-load/818.json?window=10d \ -u {email}:{authToken}`

**Response**

The main object can be ignored in this request. Note a few things:

* The requested window was 10d, which forced pagination. The length of time required to cause pagination varies based on the number of agents on a test, and the number of records returned per agent. For example, DNS Server tests are more verbose than page load tests, because they typically query multiple nameservers per agent.
* If the result set exceeds one page worth of data, `next` URL will be shown in the pages section of data. If the time range requested in the query was specified in a window format, it will be converted to from and to format (based on the original query time), to prevent missing data as you iterate through your result set.

`HTTP/1.1 200 OK Server: nginx Date: Wed, 15 Aug 2018 20:14:43 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 217 X-Organization-Rate-Limit-Reset: 1534364100 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-2`

**Body**

`{ "from": "2018-08-05 17:15:44", "pages": { "current": 1, "next": "https://api.thousandeyes.com/v6/web/page-load/818.json?lastRoundId=1533713400&from=2018-08-05+17%3A15%3A44&to=2018-08-15+17%3A15%3A44" }, "to": "2018-08-15 17:15:44", "web": {...} }`

For error responses, see the [response status codes documentation](broken-reference).

[Change policy](broken-reference)

ThousandEyes may modify the attributes and resources available to the API and our policies related to access and use of the API from time to time without advance notice. ThousandEyes will use commercially reasonable efforts to notify you of any modifications to the API or policies through notifications or posts on the ThousandEyes Customer Success Center. ThousandEyes also tracks deprecation of attributes of the API on the ThousandEyes API page, located on this site.

ThousandEyes will provide an update to the version of the API in circumstances where the structure of the API output substantively changes, format is modified, or code is deprecated.

#### Version Support <a href="#version_support" id="version_support"></a>

Support for the current and prior version of the ThousandEyes API will be provided at all times. Attempts to access the ThousandEyes API with no version specified will result in the current version being used. Attempts to access a deprecated version of the API will result in a response from the oldest supported version of the API.

**WARNING**

Version 6 is presently the current release. Version 4 will be deprecated effective Dec 26th, 2017. Based on our support statement, we support the following releases, accessible at the endpoint root specified:

* version 7 (preview, subject to change without notice): `https://api.thousandeyes.com/v7/`
* version 6 (current): `https://api.thousandeyes.com/v6/`, `https://api.thousandeyes.com/`
* version 5 (current-1): `https://api.thousandeyes.com/v5/`

#### Support Notice <a href="#support_notice" id="support_notice"></a>

New versions of the API will be released with a notification made available on our Developer reference site, and will be available using a version-specific endpoint call for a period of 90 days. After this 90-day period, the new version of the API will become the current version, and the oldest version of the API will be deprecated.

This means that the following timeline applies:

* Upon release of new API version v(X), for first 90 days:
  * Current version: v(X-1)
  * Supported versions: v(X-2)-v(X)
* After 90 days post-release of new API version
  * Current version: v(X)
  * Supported versions: v(X-1)-v(X)

[API change summary](broken-reference)

The following list documents a running list of changes to version 6 of the ThousandEyes API. Each release date is linked to the specific release notes for that release, for which Authentication is required. For details related to other versions of the ThousandEyes API, see the links on the left sidebar.

### APIv6 <a href="#apiv6" id="apiv6"></a>

[Jan 31, 2023](https://docs.thousandeyes.com/whats-new/changelog#2023-02-02)

* (removed) `verifySslCertificates` agent flag is removed.

[January 13, 2023](https://docs.thousandeyes.com/whats-new/changelog#2023-01-13)

* (removed) `Alert-Grid` widget has now been removed from the platform and from snapshots

[Dec 12, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-12-12)

* (added) Added a new endpoint for deleting endpoint agents: `/endpoint-agents/{agentId}`

[Dec 08, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-07-06)

* (added) Added the `experienceScore` field to Endpoint user session apis.

[Nov 15, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-11-15)

* (added) Web Transaction and Page Load tests have a new parameters: `blockDomains`, `disableScreenshot`, `allowMicAndCamera`, `allowGeolocation`, `browserLanguage`, `pageLoadingStrategy`.

[October 10, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-10-11)

* Reports v6 API is deprecated when dashboards and reports merge.

[Jul 06, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-07-06)

* (added) Added the `continuousMode` field to agent-to-server tests.

[Dec 08, 2021](https://docs.thousandeyes.com/whats-new/changelog#2021-12-08)

* (added) Added two new Admin APIs for obtaining & updating usage quotas

[June 23, 2021](https://docs.thousandeyes.com/whats-new/changelog#2021-06-23)

* (updated) Added documentation to indicate that `/v6/snapshots` cannot be used to create snapshots of Endpoint Agent scheduled tests.

[April 6, 2021](https://docs.thousandeyes.com/whats-new/changelog#2021-04-06)

* (added) Added a new Endpoint API for transferring agents.

[January 6, 2021](https://docs.thousandeyes.com/whats-new/changelog#2021-01-06)

* (added) `networkProtocol`, `tcpProbeMode` and `pathtraceInSession` fields added to Endpoint tests.

[September 3, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-09-03)

* (removed) `voice-call` test type is removed.

[July 10, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-07-10)

* (added) `agent-to-agent` test type now supports `pathTraceMode`

[April 28, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-04-28)

* (added) `/endpoint-agents` endpoint now supports `publicIP`, `location`, `proxy`, `agentType`, `totalMemory`, and `clients` fields.
* (added) `/endpoint-agents` endpoint allows to update an agent name.

[April 14, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-04-14)

* (added) `web-transactions` test type now supports `followRedirects` field
* (added) `/alert-rules` endpoints now support `roundsViolatingMode` field.
* (added) `/endpoint-agents` endpoint now supports `createdTime`, `lastSeen` and `version` fields.

[March 17, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-03-17)

* (added) `/tests` endpoint now supports `pathTraceMode` field.

[January 08, 2020](https://docs.thousandeyes.com/release-notes/2020/2020-01-release-notes#2020-01-08)

* (added) `/usage` endpoint now supports `EnterpriseAgentUnits` field.
* (added) `/tests` endpoints now support `dnsTransportProtocol` field.
* (removed) Device Layer licenses and usage fields from Usage metadata page as Device layer functionality is now included as a feature of the Enterprise Agent and licenses are no longer required.

[October, 03 2019](https://docs.thousandeyes.com/release-notes/2019/2019-10-03-release-notes)

* (added) write endpoints for alert rules, including `/alert-rules/new`, `alert-rules/{ruleId}/update`, and `alert-rules/{ruleId}/delete`
* (added) new metadata page for alert rules

[August 20, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-08-20-release-notes)

* (added) `/alert-rules` and `/alert-rules/{ruleId}`endpoints now support `minimumSourcesPct` field

[August 6, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-08-06-release-notes)

* (added) `/usage` endpoint now supports `enterpriseUnitsUsed`, `enterpriseUnitsProjected` and `enterpriseUnitsNextBillingPeriod` fields
* (added) `/alert-rules` endpoint now supports `direction` field
* (added) `/alert-rules` field `expression` value format has changed, from human-readable to suitable as a value for `expression` when writing to the endpoint (upcoming feature)
* (added) `/alerts` field `ruleExpression` value format has changed (in the same manner as described above)

[July 23, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-07-23-release-notes)

* (added) `/agents` and `/agents/{agentId}` endpoints now support `targetForTests` field
* (added) `/usage` endpoint now returns unit usage projection for the upcoming billing period via the `cloudUnitsNextBillingPeriod` field
* (added) `/audit/user-events/search` endpoint now returns resource data associated with the searched-for event

[April 30, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-04-30-release-notes)

* (added) `/tests` and `/tests/{testId}` endpoints now support `description` field
* (added) `/usage` endpoint now returns device and Endpoint Agent licensing information in `devicesIncluded`, `devicesUsed`, `endpointAgentsIncluded` and `endpointAgentsUsed` fields
* (added) `/agents` and `/agents/{agentId}` endpoints now return `OS_END_OF_INSTALLATION_SUPPORT` and `OS_END_OF_SUPPORT` information

[April 02, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-04-02-release-notes)

* (added) Enterprise Agent cluster management endpoints: `/agents/{agentId}/add-to-cluster` and `/agents/{agentId}/remove-from-cluster`
* (added) `/reports/{reportId}` endpoint now returns `createdBy`, `modifiedBy` and `modifiedDate` fields

[March 19, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-03-19-release-notes)

* (modified) Running instant Agent to Agent, RTP Stream and Voice Call tests is now supported

[March 6, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-03-06-release-notes)

* (added) `/tests` detailed endpoint has new parameter: `numPathTraces`

[November 27, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-11-27-release-notes)

* (modified) Agent to Agent tests created with the API now default to port 49153

November 20, 2018

* (added) Test metadata returns sharedWithAccounts element. This element shows all the Accounts Groups where a particular test is shared.

[November 13, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-11-13-release-notes)

* (added) Endpoints `/agents` and `/agents/{agentId}` now return `hostname` field

[October 23, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-10-23-release-notes)

* (added) Snapshot creation endpoint: `/snapshot`

[August 29, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-08-29-release-notes)

* (added) Endpoint Scheduled tests endpoints added
* (added) Endpoint Scheduled test data endpoints added

[August 15, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-08-15-release-notes)

* (modified) The way pagination returns the pages element has changed. The `previous` property was removed from pages element and the `next` property now uses `lastRoundId` URL parameter instead of `page` for the pagination

[August 01, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-08-01-release-notes)

* (modified) Starting August 28th, 2018, it is possible to use Cloud Agents for Instant tests.

[July 18, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-07-18-release-notes)

* (added) `/agents` and `/agents/{agentId}` includes `errorDetails` parameter when an Enterpirse Agent or Cluster Member present at least one error.
* (added) Endpoints `/agents` and `/agents/{agentId}` now return `hostname` field

[July 03, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-07-03-release-notes)

* (added) `/agents` endpoint now accepts a new querystring parameter: `agentTypes=CLOUD|ENTERPRISE|ENTERPRISE_CLUSTER`

[May 23, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-05-23-release-notes)

* (added) `/tests` detailed endpoint has new parameter: `probeMode`
* (added) Endpoint `/account-groups` now returns `organizationName` field

[May 09, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-05-09-release-notes)

* (added) HTTP Server and Page Load tests have a new parameter: `httpVersion`

[April 25, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-04-25-release-notes)

* (added) SIP Server and Voice Call tests to `/tests` endpoints.
* (added) `/voice/sip-server` endpoint now provides SIP server layer test data for both SIP Server and Voice Call tests.
* (changed) `/voice/metrics` endpoint has been renamed to `/voice/rtp-stream`, all requests to the old endpoint will be redirected with `HTTP 301`. `/voice/rtp-stream` endpoint now provides RTP stream layer test data for both RTP Stream and Voice Call tests.

[March 28, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-03-28-release-notes)

* (added) For tests which included TCP-based Network Measurements (under the Advanced Settings tab of the test configuration) you can now pick `TCP` or `ICMP` as a `protocol` when creating or editing tests.

[January 31, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-01-31-release-notes)

* We are deprecating the use of TLS 1.0 in ThousandEyes infrastructure. After tonight, clients which use only TLS 1.0 will not be able to access the API. If your client program or script is returning errors such as `The underlying connection was closed: An unexpected error occurred on a send.`, `EOF occurred in violation of protocol` or `Connection reset by peer`, you need to either upgrade your SSL libraries or ensure you are not enforcing the use of TLS 1.0.
* (added) When creating or updating a test that uses BGP monitoring, use the new `usePublicBgp` parameter set to `1` to automatically add all available Public BGP Monitors. You can continue to use the `bgpMonitors` option to assign Private BGP Monitors.
* (changed) If a public monitor is included in the `bgpMonitors` list, all public monitors will be assigned to the test, regardless of the setting specified in the `usePublicBgp` parameter.

[January 10, 2018](https://docs.thousandeyes.com/release-notes/2018/2018-01-10-release-notes)

* APIv4 has been deprecated. All queries to version 4 (`https://api.thousandeyes.com/v4/`) will receive a `HTTP 301` redirect to the oldest supported API version (currently version 5).

[November 8, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-11-08-release-notes)

* (added) `/report-snapshots` endpoint has new parameters: `shared` and `timeSpan`
* (changed) `/alert-rules` detailed endpoint `notes` and `recipient` parameters moved under `notifications.email`, `notes` renamed to `message`

[October 12, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-10-12-release-notes)

* (added) `/dns/trace` endpoint has new parameters: `failedQueries` and `finalServerQueried`
* (added) `/net/path-vis` endpoint has new parameters: `sourceIp` and `sourcePrefix`

[September 27, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-09-27-release-notes)

* (added) APIv6 is now default version. All queries without explicit version (`https://api.thousandeyes.com/` instead of `https://api.thousandeyes.com/v5/`) will receive version 6 response.
* 90-day countdown for APIv4 deprecation begins with a target date of December 26, 2017. Please refer to the [versioning](broken-reference) page for details.
* (added) Agent endpoints `agentState` parameter now has a third state: `Disabled`

[July 7, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-07-07-release-notes)

* (added) Activity Log endpoint: `/audit/user-events/search`

[June 6, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-06-06-release-notes)

* (added) Agent Detail endpoint now provides Enterprise Cluster utilization
* (announced) destructive change freeze for APIv6 - after today’s release, no future changes will result in a destructive change to the schema.
* (revised announcement) 90-day countdown for APIv6 moving to default begins June 7, 2017, with a target date of September 13, 2017. Please refer to the [versioning](broken-reference) page for details.

[April 26, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-04-26-release-notes)

* (added) Agent Notification Rules endpoint: `/agent-notification-rules`
* (added) Agent Notification Rule Detail endpoint: `/agent-notification-rules/{ruleId}`
* (announced) target date for change of current API version is May 24, 2017. Current version will be changed from v5 to v6, and 90-day clock for APIv4 has started.

[April 12, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-04-12-release-notes)

* (changed) alert rules endpoint changed: removed recipients from this endpoint in favor of adding `/alert-rules/{ruleId}` endpoint, which lists alert recipients of all types, including Slack, PagerDuty and generic webhooks
* (added) Alert rule detail endpoint: `/alert-rules/{ruleId}`
* (added) Alert Suppression Window list `/alert-suppression-windows`
* (added) Alert Suppression Window detail `/alert-suppression-windows/{alertSuppressionWindowId}`
* (added) Alert Suppression Window creation `/alert-suppression-windows/new`
* (added) Alert Suppression Window deletion `/alert-suppression-windows/{alertSuppressionWindowId}/delete` endpoint
* (added) Alert Suppression Window modification `/alert-suppression-windows/{alertSuppressionWindowId}/update` endpoint
* (added) integrations list endpoint `/integrations`
* (added) Endpoint user session list `/endpoint-data/user-sessions`
* (added) Endpoint user session details `/endpoint-data/user-sessions/{sessionId}`
* (added) Endpoint web page list `/endpoint-data/user-sessions/{sessionId}/web`
* (added) Endpoint web page details `/endpoint-data/user-sessions/{sessionId}/page/{pageId}`
* (added) Endpoint network sessions list `/endpoint-data/user-sessions/{sessionId}/network`
* (added) Endpoint network topology list `/endpoint-data/network-topology`
* (added) Endpoint network topology detail `/endpoint-data/network-topology/{networkProbeId}`
* (added) Endpoint agent list `/endpoint-agents/`
* (added) Endpoint agent details `/endpoint-agents/{agentId}`
* (added) Endpoint networks `/endpoint-data/networks`
* (added) several report snapshot list `/report-snapshots`
* (added) several report snapshot detail `/report-snapshots/{snapshotId}`
* (added) several report snapshot data `/report-snapshots/{snapshotId}/{dataComponentId}`
* (added) several report snapshot deletion `/report-snapshots/{snapshotId}/delete`
* (changed) removed BETA badge from reports endpoints (no longer in beta)

[March 15, 2017](https://docs.thousandeyes.com/release-notes/2017/2017-03-15-release-notes)

* (added) Instant Tests 2.0 documentation is [now available](../.gitbook/assets/instant)
* (added) documentation for FTP server tests to `/web/ftp-server/{testId}`
* (fixed) some metadata in table listed in the Transaction Detail endpoint was offset by a column.

[November 23, 2016](https://docs.thousandeyes.com/release-notes/2016/2016-11-23-release-notes)

* (added) `/reports` endpoint
* (added) `/reports/{reportId}` endpoint
* (added) `/reports/{reportId}/{dataComponentId}` endpoint
* (fixed) problems with setting advanced options on some test creation endpoints
* (added) `pingPayloadSize` field added to network tests
* (added) `lastLogin` field to `/users` endpoint
* (added) `dateRegistered` field to `/users` endpoint
* (added) oAuth support for API queries: see [Authentication](broken-reference) for more details.

[August 31, 2016](https://docs.thousandeyes.com/release-notes/2016/2016-08-31-release-notes)

* (added) `/tests/ftp-server` endpoint added (filter all tests on FTP server tests)
* (added) `/web/ftp-server/{testId}` endpoint added (return results for FTP server tests)
* (added) `X-Organization-Rate-Limit-Limit`, `X-Organization-Rate-Limit-Remaining`, and `X-Organization-Rate-Limit-Reset` headers added to requests to handle rate limit control
* (added) `followRedirects` (boolean) element to HTTP Server tests

[July 20, 2016](https://docs.thousandeyes.com/release-notes/2016/2016-07-20-release-notes)

* (changed) added no-cache directive to responses from the ThousandEyes API to prevent content from being cached on proxy servers
* (added) `dnsOverride`, `clientCertificate` `desiredStatusCode` advanced options for HTTP Server test setting endpoints

[July 6, 2016](https://docs.thousandeyes.com/release-notes/2016/2016-07-06-release-notes)

* (changed) moved `type` attribute of XML representation of alerts endpoint to a child element.
* (changed) `fetchTime` in HTTP Server results endpoint changed to `totalTime`
* (added) implemented burst limit for instant test API calls
* (changed) calling `/net/path-vis/{testId}` and `/net/path-vis/{testId}/{agentId}/{roundId}` for agent to agent tests with direction parameter of BIDIRECTIONAL will now throw an error (http/400 status code)
* (added) agent `hostname` to `/agents` and `/agents/{agentId}` endpoints
* (changed) `roundsBeforeTrigger` field has been removed from alert rules, and replaced with `roundsViolatingRequired` and `roundsViolatingOutOf`, respectively.

[June 8, 2016](https://docs.thousandeyes.com/release-notes/2016/2016-06-08-release-notes)

* (added) countryID field to `/net/metrics` endpoint
* (added) errorDetails field to `/net/metrics` endpoint
* (fixed) changed default behavior when querying `/net/metrics` and `/net/path-vis` endpoints for agent to agent tests. In the case of bidirectional tests, the `/net/metrics` endpoint will return aggregate information for both directions - specifying a direction as a querystring parameter `direction=[FROM_TARGET | TO_TARGET]` will return that direction’s metrics specifically. For the `/net/path-vis` endpoint, each direction must be queried independently. Specifying an invalid direction will result in an error response.

[May 25, 2016](https://docs.thousandeyes.com/release-notes/2016/2016-05-25-release-notes)

* Preview for APIv6 launched
* (changed) Accounts are now shown as account-groups. The `/accounts` endpoint has been replaced with `/account-groups`
* (changed) Network tests have been replaced with agent-to-server tests, and agent-to-agent tests. This is now reflected under the type field for tests
* (added) `/tests/agent-to-server` endpoint
* (added) `/tests/agent-to-agent` endpoint
* (removed) `/tests/network` endpoint
* (added) direction parameter to results endpoints (`net/metrics`, `net/path-vis`) for agent-to-agent tests
* (added) Account Group, Role, and User management endpoints
* (added) Usage endpoint
