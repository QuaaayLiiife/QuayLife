# Reports

### Reports

[`GET /v6/reports` Reports list](broken-reference)

This endpoint returns a list of reports configured in ThousandEyes in the context of the user’s current account group. This endpoint requires the `View Reports` permission be assigned to the role of the user accessing this endpoint. Use this data to find a report in your account, which is then used in other endpoint to access aggregated data.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/reports.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of reports configured in the current account group. Each report contains the following fields:

| Field Name | Data Type                | Notes                                                          |
| ---------- | ------------------------ | -------------------------------------------------------------- |
| reportId   | string                   | unique Id of the report                                        |
| reportName | string                   | name of the report                                             |
| builtIn    | boolean                  | 1 for built-in reports, 0 for user-created reports             |
| apiLinks   | array of apiLink objects | a list of links which can be followed to pull more information |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 21 Nov 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "reports: [ { "apiLinks": [...], "builtIn": 1, "reportId": "2", "reportName": "ThousandEyes Built-in: HTTP Server" }, { "apiLinks": [...], "builtIn": 1, "reportId": "1", "reportName": "ThousandEyes Built-in: Network Layer" }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/reports/{reportId}` Report detail](broken-reference)

This endpoint returns a list of widgets configured in reports configured in ThousandEyes. Seed this endpoint with a reportId found from the /reports endpoint. This endpoint requires the `View Reports` permission be assigned to the role of the user accessing this endpoint.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{reportId}` the ID of the report you’re interested in.

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/reports/590ca0db90b0357f7e8ae1ad.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns report metadata information and associated widget list. Each widget will show a list of data components shown in the widget. Each data component includes a metric, measure, and grouping information, as well as details around any embeddings which exist for the widget:

| Field Name   | Data Type                | Notes                                                                                    |
| ------------ | ------------------------ | ---------------------------------------------------------------------------------------- |
| reportId     | string                   | unique ID of the report                                                                  |
| reportName   | string                   | name of the report                                                                       |
| createdBy    | integer                  | ID of the user who created the report, as returned by the `/v6/users` API endpoint       |
| modifiedBy   | integer                  | ID of the user who last modified the report, as returned by the `/v6/users` API endpoint |
| modifiedDate | string                   | YYYY-MM-DD HH:mm:ss formatted date of last report modification time, shown in UTC        |
| builtIn      | boolean                  | 1 for built-in reports, 0 for user-created reports                                       |
| apiLinks     | array of apiLink objects | a list of links which can be followed to pull more information                           |
| widgets      | array                    | an array of widget objects                                                               |

Each widget object has the following fields:

| Field Name     | Data Type | Notes                                                                                                                                  |
| -------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| title          | string    | widget title                                                                                                                           |
| type           | string    | widget type; `table`, `multi-metric-table`, `geomap`, `numbers`, `pie-chart`, `timeseries`, `stacked-areachart`, `box-and-whiskers`, … |
| dataComponents | array     | array of widget data components                                                                                                        |
| embedUrl       | string    | if widget is marked as embedded, embedUrl is provided                                                                                  |

Each widget is comprised of one or more data components, fields represented by the following table:

| Field Name      | Data Type                | Notes                                                                                                                                                                                                                                                                                                                                 |
| --------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataComponentId | string                   | unique ID of the data component. Use this value to retrieve dataComponent values.                                                                                                                                                                                                                                                     |
| metric          | string                   | the metric being tabulated in the report: defined by the layer, test type and metric.                                                                                                                                                                                                                                                 |
| measure         | string                   | statistical measure shown, i.e. `Minimum`, `Maximum`, …                                                                                                                                                                                                                                                                               |
| groupBy         | array of groupBy objects | array of `groupBy` strings, i.e. `Tests`, `Agents`, …                                                                                                                                                                                                                                                                                 |
| filters         | array of filter objects  | (optional) where the widget is filtered, filters property is shown. Each filter object represents one selected item and contains `filterProperty` and `filterValue` properties. `filterProperty` can be `Agents`, `Agent Groups`, `Tests`, `Monitors`, etc. `filterValue` holds the Id of the property, i.e. test, agent, monitor Id. |
| fixedTimeSpan   | number                   | (optional) where widget timespan is different from report’s timespan, this parameter is set to number of seconds in the timespan                                                                                                                                                                                                      |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 21 Nov 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "reports": [ { "apiLinks": [...], "builtIn": 1, "reportId": "2", "reportName": "ThousandEyes Built-in: HTTP Server", "widgets": [ { "dataComponents": [ { "apiLinks": [...], "dataComponentId": "vlvb1", "description": "Average Availability", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Availability" }, { "apiLinks": [...], "dataComponentId": "dyivi", "description": "Average Response Time", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Response Time" }, ... ], "title": "HTTP Server Overview", "type": "numbers" }, { "dataComponents": [ { "apiLinks": [ { "href": "https://api.thousandeyes.com/v6/reports/590ca0db90b0357f7e8ae1ad/ynubv", "rel": "data" } ], "dataComponentId": "ynubv", "filters": [ { "filterProperty": "Tests", "filterValue": "817" }, { "filterProperty": "Tests", "filterValue": "818" } ], "groupBy": [ "Agents" ], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Availability" } ], "title": "Overall Average Availability", "type": "timeseries" }, ... ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/reports/{reportId}/{dataComponentId}` Report data](broken-reference)

This endpoint returns actual metrics used in the generation of the reports shown. Unlike the metadata options, this endpoint accepts parameters for a time range shown in the data, which defaults to 7 days.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.
* `{reportId}` the ID of the report you’re interested in.
* `{dataComponentId}` the ID of the data component for which to retrieve data.

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/reports/2/vlvb1.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back a list of data elements associated with the report. The data components are aggregated by our services, then reported back in bins: each bin represents a point on the chart: the granularity of the points shown in the chart is based on the data range shown in the report. Bin sizes are based on the table below:

| Report time range | Bin size  |
| ----------------- | --------- |
| up to 1 day       | 5 minutes |
| 1 day - 14 days   | 1 hour    |
| 15 days - 30 days | 2 hours   |
| 31 days - 50 days | 4 hours   |
| 51 days - 93 days | 6 hours   |

If your data is grouped, a value will be shown for each data grouping for each bin. Corresponding data is returned according to the following fields:

| Field Name                  | Data Type                      | Notes                                                                                                                                               |
| --------------------------- | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| from                        | dateTime                       | the start of the data shown in the API output                                                                                                       |
| to                          | dateTime                       | end of the data window shown in the API output                                                                                                      |
| data.binId                  | integer                        | corresponds to the start time for the bin                                                                                                           |
| data.count                  | integer                        | number of datapoints shown in the round                                                                                                             |
| data.value                  | float                          | value of the datapoint                                                                                                                              |
| data.groups                 | array of group objects         | this corresponds to how the data is labelled in the widget. Match the groupProperty and groupId to retrieve the label as represented in the widget. |
| groupLabelMaps              | array of groupLabelMap objects | see groupLabelMap fields below                                                                                                                      |
| groupLabelMap.groupProperty | string                         | matches the groupProperty listed in the data.groups object                                                                                          |
| groupLabelMap.groupLabels   | array of groupLabel objects    | see individual fields below                                                                                                                         |
| groupLabel.groupId          | string                         | lookup value of the group                                                                                                                           |
| groupLabel.groupLabel       | string                         | value of the legend                                                                                                                                 |
| binSize                     | integer                        | duration of each bin                                                                                                                                |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 21 Nov 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "from": "2017-04-25 14:00:00", "to": "2017-05-02 14:00:00", "reportDataComponentData": { "binSize": 3600, "data": [ { "binId": 1492524000, "count": 5376, "value": 99.90699404761905 }, { "binId": 1493730000, "count": 5376, "value": 99.7953869047619 } ], "groupLabelMaps":[ { "groupProperty":"Tests", "groupLabels":[ { "groupId":"29697", "groupLabel":"http://jackli.design" }, { "groupId":"1580", "groupLabel":"OLD Periodic Failure Example" } ] } ], } }` For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/reports/{reportId}/delete` Deleting a report](broken-reference)

Deletes the specified report in ThousandEyes, based on the reportId provided in the API request. Users with the `Edit reports for all users in account group` permission (Account Admin) can delete any report. Users with `Edit own reports` permission (Regular User) can only delete the reports they have created.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{reportId}` the ID of the report you would like to delete

#### Response <a href="#response" id="response"></a>

If the report is successfully deleted, an HTTP 204 NO CONTENT response will be returned. If user lacks the permissions to delete the report, an HTTP 401 UNAUTHORIZED response will be returned.

Response has no body.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/reports/58c9437149b02d5410fd06cd/delete.json \ -d '' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Server: nginx Date: Wed, 15 Mar 2017 13:47:45 GMT Content-Type: application/json;charset=UTF-8 Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1489585680 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/report-snapshots` Report snapshots list](broken-reference)

This endpoint returns a list of report snapshots configured in ThousandEyes in the context of the user’s current account group. This endpoint requires the `View Reports` permission be assigned to the role of the user accessing this endpoint. Use this data to find a report snapshot in your account, which is then used in other endpoint to access aggregated data.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/report-snapshots.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of report snapshots configured in the current account group. Each report snapshot object contains the following fields:

| Field Name         | Data Type                | Notes                                                          |
| ------------------ | ------------------------ | -------------------------------------------------------------- |
| snapshotId         | string                   | unique ID of the report snapshot                               |
| snapshotName       | string                   | name of the report snapshot                                    |
| createdDate        | dateTime                 | the date/time when report snapshot was created                 |
| scheduled          | boolean                  | 1 if report snapshot was generated from a schedule             |
| shared             | boolean                  | 1 if report snapshot is shared                                 |
| report             | object                   | report this report snapshot is based upon                      |
| report.reportId    | string                   | unique ID of the report                                        |
| report.reportName  | string                   | name of the report                                             |
| report.builtIn     | boolean                  | 1 for built-in reports, 0 for user-created reports             |
| report.apiLinks    | array of apiLink objects | a list of links which can be followed to pull more information |
| timespan.startDate | dateTime                 | the date/time of beginning of report snapshot                  |
| timespan.duration  | integer                  | duration of report snapshot in seconds                         |
| permalink          | string                   | link to report snapshot in ThousandEyes Application            |
| apiLinks           | array of apiLink objects | a list of links which can be followed to pull more information |

`HTTP/1.1 200 OK Server: nginx Date: Thu, 13 Apr 2017 09:38:58 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076340 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "pages": { "current": 1 }, "reportSnapshots": [ { "apiLinks": [...], "createdDate": "2017-05-02 14:42:49", "permalink": "https://app.thousandeyes.com/reports/snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2?__a=75", "report": { "apiLinks": [...], "builtIn": 1, "reportId": "2", "reportName": "ThousandEyes Built-in: HTTP Server" }, "scheduled": 0, "shared": 0, "snapshotId": "60886ebb-2466-444d-bbd8-74d5ea1402d2", "snapshotName": "HTTP Server Report Snapshot", "timeSpan": { "duration": 604800, "startDate": "2017-03-15 00:00:00" } }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/report-snapshots/{snapshotId}` Report snapshot detail](broken-reference)

This endpoint returns a list of widgets configured in reports configured in ThousandEyes. Seed this endpoint with a reportId found from the /reports endpoint. This endpoint requires the `View Reports` permission be assigned to the role of the user accessing this endpoint.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{snapshotId}` the ID of the report snapshot you’re interested in.

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/report-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns details information about report snapshot including the list and configuration of the widgets.

| Field Name         | Data Type                | Notes                                                          |
| ------------------ | ------------------------ | -------------------------------------------------------------- |
| snapshotId         | string                   | unique ID of the report snapshot                               |
| snapshotName       | string                   | name of the report snapshot                                    |
| createdDate        | dateTime                 | the date/time when report snapshot was created                 |
| scheduled          | boolean                  | 1 if report snapshot was generated from a schedule             |
| shared             | boolean                  | 1 if report snapshot is shared                                 |
| report             | object                   | report this report snapshot is based upon                      |
| report.reportId    | string                   | unique ID of the report                                        |
| report.reportName  | string                   | name of the report                                             |
| report.builtIn     | boolean                  | 1 for built-in reports, 0 for user-created reports             |
| report.apiLinks    | array of apiLink objects | a list of links which can be followed to pull more information |
| timespan.startDate | dateTime                 | the date/time of beginning of report snapshot                  |
| timespan.duration  | integer                  | duration of report snapshot in seconds                         |
| permalink          | string                   | link to report snapshot in ThousandEyes Application            |
| apiLinks           | array of apiLink objects | a list of links which can be followed to pull more information |
| widgets            | array                    | an array of widget objects                                     |

Each widget object has the following fields:

| Field Name     | Data Type | Notes                                                                                                                                  |
| -------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| title          | string    | widget title                                                                                                                           |
| type           | string    | widget type; `table`, `multi-metric-table`, `geomap`, `numbers`, `pie-chart`, `timeseries`, `stacked-areachart`, `box-and-whiskers`, … |
| dataComponents | array     | array of widget data components                                                                                                        |
| embedUrl       | string    | if widget is marked as embedded, embedUrl is provided                                                                                  |

Each widget is comprised of one or more data components, fields represented by the following table:

| Field Name      | Data Type                | Notes                                                                                                                                                                                                                                                                                                                                 |
| --------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataComponentId | string                   | unique ID of the data component                                                                                                                                                                                                                                                                                                       |
| metric          | string                   | the metric being tabulated in the report: defined by the layer, test type and metric.                                                                                                                                                                                                                                                 |
| measure         | string                   | statistical measure shown, i.e. `Minimum`, `Maximum`, …                                                                                                                                                                                                                                                                               |
| groupBy         | array                    | array of `groupBy` strings, i.e. `Tests`, `Agents`, …                                                                                                                                                                                                                                                                                 |
| filters         | array of filter objects  | (optional) where the widget is filtered, filters property is shown. Each filter object represents one selected item and contains `filterProperty` and `filterValue` properties. `filterProperty` can be `Agents`, `Agent Groups`, `Tests`, `Monitors`, etc. `filterValue` holds the Id of the property, i.e. test, agent, monitor Id. |
| apiLinks        | array of apiLink objects | a list of links which can be followed to pull more information                                                                                                                                                                                                                                                                        |

`HTTP/1.1 200 OK Server: nginx Date: Thu, 13 Apr 2017 09:41:13 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "reportSnapshots": [ { "apiLinks": [...], "createdDate": "2017-05-02 14:42:49", "permalink": "https://app.thousandeyes.com/reports/snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2?__a=75", "report": { "apiLinks": [...], "builtIn": 1, "reportId": "2", "reportName": "ThousandEyes Built-in: HTTP Server" }, "scheduled": 0, "shared": 0, "snapshotId": "60886ebb-2466-444d-bbd8-74d5ea1402d2", "snapshotName": "HTTP Server Report Snapshot", "timeSpan": { "duration": 604800, "startDate": "2017-03-15 00:00:00" }, "widgets": [ { "dataComponents": [ { "apiLinks": [...], "dataComponentId": "59089917755cb04ee9944e44", "description": "Average Availability", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Availability" }, { "apiLinks": [...], "dataComponentId": "59089ae6755cb04ee977703b", "description": "Average Response Time", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Response Time" }, ... ], "title": "HTTP Server Overview", "type": "numbers" }, { "dataComponents": [ { "apiLinks": [...], "dataComponentId": "590897e4755cb04ee9776f5b", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Availability" } ], "title": "Overall Average Availability", "type": "timeseries" }, ... ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/report-snapshots/{snapshotId}/{dataComponentId}` Report snapshot data](broken-reference)

This endpoint returns actual metrics used in the generation of the report snapshot shown.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.
* `{snapshotId}` the ID of the report snapshot you’re interested in.
* `{dataComponentId}` the ID of the data component for which to retrieve data.

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/report-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2/59089917755cb04ee9944e44.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back a list of data elements associated with the report snapshot. The data components are aggregated by our services, then reported back in bins: each bin represents a point on the chart: the granularity of the points shown in the chart is based on the data range shown in the report snapshot. Bin sizes are based on the table below:

| Report time range | Bin size  |
| ----------------- | --------- |
| up to 1 day       | 5 minutes |
| 1 day - 14 days   | 1 hour    |
| 15 days - 30 days | 2 hours   |
| 31 days - 50 days | 4 hours   |
| 50 days - 93 days | 6 hours   |

If your data is grouped, a value will be shown for each data grouping for each bin. Corresponding data is returned according to the following fields:

| Field Name              | Data Type | Notes                                          |
| ----------------------- | --------- | ---------------------------------------------- |
| from                    | dateTime  | the start of the data shown in the API output  |
| to                      | dateTime  | end of the data window shown in the API output |
| reportDataComponentData | object    | object represents report data component data   |

`reportDataComponentData` object has the following fields:

| Field Name                  | Data Type                      | Notes                                                                                                                                              |
| --------------------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| data.binId                  | integer                        | corresponds to the start time for the bin                                                                                                          |
| data.count                  | integer                        | number of datapoints shown in the round                                                                                                            |
| data.value                  | float                          | value of the datapoint                                                                                                                             |
| data.groups                 | array of group objects         | this corresponds to how the data is labelled in the widget. Match the groupProperty and groupId o retrieve the label as represented in the widget. |
| groupLabelMaps              | array of groupLabelMap objects | see groupLabelMap fields below                                                                                                                     |
| groupLabelMap.groupProperty | string                         | matches the groupProperty listed in the data.groups object                                                                                         |
| groupLabelMap.groupLabels   | array of groupLabel objects    | see individual fields below                                                                                                                        |
| groupLabel.groupId          | integer                        | lookup value of the group                                                                                                                          |
| groupLabel.groupLabel       | string                         | value of the legend                                                                                                                                |
| binSize                     | integer                        | duration of each bin                                                                                                                               |

`HTTP/1.1 200 OK Server: nginx Date: Thu, 13 Apr 2017 14:29:51 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1492093800 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "from": "2017-03-15 00:00:00", "to": "2017-03-22 00:00:00", "reportDataComponentData": { "binSize": 3600, "data": [ { "binId": 1492002000, "count": 10042, "groups": [ { "groupProperty": "Continents", "groupValue": "APNIC" } ], "value": 4236.95 }, { "binId": 1492002000, "count": 16112, "groups": [ { "groupProperty": "Continents", "groupValue": "ARIN" } ], "value": 3801.1 }, ... ], "groupLabelMaps": [] }, }` For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/report-snapshots/{snapshotId}/delete` Deleting a report snapshot](broken-reference)

Deletes the specified report snapshot in ThousandEyes, based on the snapshotId provided in the API request. Users with the `Edit reports for all users in account group` permission (Account Admin) can delete any report snapshot. Users with `Edit own reports` permission (Regular User) can only delete the report snapshots for reports they have created.

***

> **WARNING**: The v6 reports API is deprecated. Please use the [dashboards](https://developer.thousandeyes.com/v6/dashboards/) API instead.

***

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{snapshotId}` the ID of the report snapshot you would like to delete

#### Response <a href="#response" id="response"></a>

If the report snapshot is successfully deleted, an HTTP 204 NO CONTENT response will be returned. If user lacks the permissions to delete the report, an HTTP 401 UNAUTHORIZED response will be returned.

Response has no body.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/report-snapshot/2bee381c-cc97-49f4-9ef5-1013c97f4124/delete.json \ -d '' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Server: nginx Date: Thu, 13 Apr 2017 09:43:28 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
