# ThousandEyes Developer Reference v7

This is a preview of our upcoming API version 7, subject to [change](broken-reference) without notice.\
At this time, [APIv6](https://developer.thousandeyes.com/v6) is the recommended API version to use.

### Overview

[Welcome](broken-reference)

Most applications will use an existing wrapper library in the language of your choice. Over the past several months, we’ve had discussions with customers using LINQ, Microsoft .NET, Python and Java to access our API content.

That said, it’s important to get familiar with the underlying methods used in the API before getting your hands dirty.

For simplicity’s sake, we’ll use cURL for documenting examples, and outputs will be shown in JSON (because it’s less verbose than XML and lends itself more readily to readability) - see [response formats](broken-reference) for more detailed information on controlling output format.

Let’s start by accessing an information-only API endpoint.

`$ curl https://api.thousandeyes.com/v7/status.json`

**Output**

This returns the current controller time (in epoch format), if run correctly. This is simply intended for verification that the API is currently running.

`{"timestamp":1492606869263}`

Let’s show the response headers, using the -i flag:

`$ curl -i https://api.thousandeyes.com/v7/status.json`

**Output**

Most of the headers are inconsequential - you’ll see the server’s date and time, version, http status code for your request. When working with our API programmatically, always check to make sure you receive an HTTP/200 response code to your request.

`HTTP/1.1 200 OK Server: nginx Date: Wed, 19 Apr 2017 13:01:09 GMT Content-Type: text/xml Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-5`

`{"timestamp":1492606869263}`

For information on our HTTP status responses, see the [response status codes documentation](broken-reference).

[Authentication](broken-reference)

The ThousandEyes API accepts OAuth bearer token as authentication methods. This is specified using the HTTP request wrapper of your choice. The OAuth Bearer Token referenced here and throughout the developer reference is available from your [account settings page](https://app.thousandeyes.com/settings/account/?section=profile) under the “Profile” tab, in the “User API Tokens” section.

The following example leverages cURL presenting a bearer token:

`$ curl -i https://api.thousandeyes.com/v7/tests.json \ --header "Authorization: Bearer {authToken}"`

For bearer token authentication, the parameter can only be read in the header in the form `Authorization: Bearer <token string>`

### Powershell Syntax <a href="#powershell_syntax" id="powershell_syntax"></a>

We’ve been asked by a number of people how to effectively create and leverage credentials against the API in Windows Powershell. When leveraging the bearer token, the token itself can be passed directly as a string:

`[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 $apitoken = "{bearerToken}" $headers = @{"accept"= "application/json"; "content-type"= "application/json"; "authorization"= "Bearer " + $apitoken} $response = Invoke-WebRequest https://api.thousandeyes.com//v7/tests.json -Headers $headers $response.content`

NOTE: The OAuth Bearer Token is available from your [account settings page](https://app.thousandeyes.com/settings/account/?section=profile) under the “Profile” tab, in the “User API Tokens” section.

### Account Lockout <a href="#account_lockout" id="account_lockout"></a>

You account could be locked up due to a number of failed authentication attempts into the ThousandEyes application.

If attempts to reach the API are returning an `401 UNAUTHORIZED` response code, but your credentials are correct it is possible that your account is locked up. Try logging into the App, it your account is locked up, you will be required to reset your password.

### Source IP block <a href="#source_ip_block" id="source_ip_block"></a>

When 120 or more unauthorized requests (resulting in the `401 UNAUTHORIZED` response) are issued from a given source IP address within an hour, API server will start responding with the `429 TOO MANY REQUESTS` response code. Your API script should handle `401 UNAUTHORIZED` error and prevent further requests to avoid the source IP block.

For error responses, see the [response status codes documentation](broken-reference).

[`GET /v7/account-groups` Account group context](broken-reference)

Users assigned to multiple account groups can change account group context by using the `aid={aid}` parameter. A list of account group IDs can be found using the [Account group list](http://developer.thousandeyes.com/v7/admin/#/accountgroup\_list) endpoint.

[Response formats](broken-reference)

Current version of the ThousandEyes API allows output in the following formats:

* JSON (JavaScript Object Notation)
* XML (Extensible Markup Language) [Schema document can be downloaded here](https://api.thousandeyes.com/v7/docs/te-api-v7.xsd)

It is possible to control the output of the API’s results using the following options, in descending order of precedence.

In the event that multiple, conflicting formats are specified, the order of precedence is:

1. Request
2. Accept Header
3. Querystring Parameter.

#### Append format to request <a href="#append_format_to_request" id="append_format_to_request"></a>

Appending either .xml or .json to the request will return the response in that type.

* to request a JSON response:

`$ curl https://api.thousandeyes.com/v7/tests.json \ -u {email}:{authToken}`

* to request an XML response:

`$ curl https://api.thousandeyes.com/v7/tests.xml \ -u {email}:{authToken}`

Modifying the header to accept different response types is the approach which will be most effective for guaranteeing the response type.

* `Accept:application/json` will return the response in JSON
* `Accept:text/xml` will return the response in XML

`$ curl -H "Accept: application/json" https://api.thousandeyes.com/v7/tests \ -u {email}:{authToken}`

#### QueryString Parameter <a href="#querystring_parameter" id="querystring_parameter"></a>

Appending a `format` parameter to the end of a QueryString will change the response format. The parameter and values must be in lowercase. Acceptable options:

* format=xml
* format=json

`$ curl https://api.thousandeyes.com/v7/tests?format=json \ -u {email}:{authToken}`

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
| 201         | CREATED                | Using the `/tests/{testType}/new` endpoint                                                                   |
| 204         | NO CONTENT             | Using the `/tests/{testType}/{testId}/delete` endpoint                                                       |
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

`$ curl -i https://api.thousandeyes.com/v7/web/page-load/818.json?window=10d \ -u {email}:{authToken}`

**Response**

The main object can be ignored in this request. Note a few things:

* The requested window was 10d, which forced pagination. The length of time required to cause pagination varies based on the number of agents on a test, and the number of records returned per agent. For example, DNS Server tests are more verbose than page load tests, because they typically query multiple nameservers per agent.
* If the result set exceeds one page worth of data, `next` URL will be shown in the pages section of data. If the time range requested in the query was specified in a window format, it will be converted to from and to format (based on the original query time), to prevent missing data as you iterate through your result set.

`HTTP/1.1 200 OK Server: nginx Date: Wed, 15 Aug 2018 20:14:43 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 217 X-Organization-Rate-Limit-Reset: 1534364100 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-2`

**Body**

`{ "from": "2018-08-05 17:15:44", "pages": { "current": 1, "next": "https://api.thousandeyes.com/v7/web/page-load/818.json?lastRoundId=1533713400&from=2018-08-05+17%3A15%3A44&to=2018-08-15+17%3A15%3A44" }, "to": "2018-08-15 17:15:44", "web": {...} }`

For error responses, see the [response status codes documentation](broken-reference).

[Change policy](broken-reference)

ThousandEyes may modify the attributes and resources available to the API and our policies related to access and use of the API from time to time without advance notice. ThousandEyes will use commercially reasonable efforts to notify you of any modifications to the API or policies through notifications or posts on the ThousandEyes Customer Success Center. ThousandEyes also tracks deprecation of attributes of the API on the ThousandEyes API page, located on this site.

ThousandEyes will provide an update to the version of the API in circumstances where the structure of the API output substantively changes, format is modified, or code is deprecated.

#### Version Support <a href="#version_support" id="version_support"></a>

Support for the current and prior version of the ThousandEyes API will be provided at all times. Attempts to access the ThousandEyes API with no version specified will result in the current version being used. Attempts to access a deprecated version of the API will result in a response from the oldest supported version of the API.

**WARNING**

Version 6 is presently the current release. Based on our support statement, we support the following releases, accessible at the endpoint root specified:

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

The following list documents a running list of changes to version 7 of the ThousandEyes API. Each release date is linked to the specific release notes for that release, for which Authentication is required. For details related to other versions of the ThousandEyes API, see the links on the left sidebar.

### APIv7 <a href="#apiv7" id="apiv7"></a>

[January 13, 2023](https://docs.thousandeyes.com/whats-new/changelog#2023-01-13)

* (removed) `Alert-Grid` widget has now been removed from the platform and from snapshots

[October 10, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-10-11)

* Reports v7 API is deprecated when dashboards and reports merge.

[June 24, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-06-24)

* (added) Alert details endpoint now returns list of affected tests for `network-outage` alerts

[April 28, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-04-28)

* (added) New [alert endpoints](../.gitbook/assets/alerts) added, at `/v7/alerts`, with support for Internet Insights outage alerts

[February 04, 2020](https://docs.thousandeyes.com/whats-new/changelog#2020-02-04)

* (added) New dashboard endpoints, at `/v7/dashboard`

[November 26, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-11-26-release-notes)

* (updated) Path visualization endpoint now returns complete data at once

[October 15, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-10-15-release-notes)

* (updated) Reports endpoints have been updated with new functionality and structure, at `/v7/reports`

[October 01, 2019](https://docs.thousandeyes.com/release-notes/2019/2019-10-03-release-notes)

* Preview for APIv7 launched
