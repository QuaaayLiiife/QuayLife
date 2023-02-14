# DASHBOARDS

This is a preview of our upcoming API version 7, subject to [change](https://developer.thousandeyes.com/v7/#/changesummary) without notice.\
At this time, [APIv6](https://developer.thousandeyes.com/v6) is the recommended API version to use.

### Dashboards

[`GET /v7/dashboards` Dashboard list](broken-reference)

This endpoint returns a list of dashboards configured in ThousandEyes in the context of the user’s login account group. Use this response to find a dashboard in your account group, which can be used to pull data of the specific dashboard.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group. Specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Response <a href="#response" id="response"></a>

Sends back an array of dashboards configured in the current account group. Each dashboard contains the following fields:

| Field Name          | Data Type | Notes                                                                                                                                                                                                               |
| ------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dashboardId         | string    | Unique ID of the dashboard                                                                                                                                                                                          |
| title               | string    | Title of the dashboard                                                                                                                                                                                              |
| description         | string    | A longer text explanation of what the dashboard does intended for the user. This field will be shown as text only. It may be used as help for other users but is not typically displayed when showing the dashboard |
| isBuiltIn           | boolean   | True for built-in dashboards, false for user-created dashboards                                                                                                                                                     |
| accountId           | integer   | ID of the account that the dashboard belongs to                                                                                                                                                                     |
| createdBy           | integer   | ID of the user that created the dashboard                                                                                                                                                                           |
| modifiedBy          | integer   | ID of the user that last modified the dashboard                                                                                                                                                                     |
| modifiedDate        | dateTime  | The date/time when the dashboard was last modified                                                                                                                                                                  |
| isPrivate           | boolean   | The dashboard can be viewed by other users in the account. If true, only the creator of the dashboard may view it. If false, all users in the same account may view it.                                             |
| isDefaultForUser    | boolean   | True if this dashboard is the default for the user, false otherwise                                                                                                                                                 |
| isDefaultForAccount | boolean   | True if this dashboard is the default for the account group, false otherwise                                                                                                                                        |
| defaultTimespan     | object    | Default timespan value to override widget timespans, see `defaultTimespan` below for details                                                                                                                        |
| globalOverride      | boolean   | True to override widget timespans and use defaultTimespan                                                                                                                                                           |
| isMigratedReport    | boolean   | True if this dashboard was previously a report                                                                                                                                                                      |
| apiLink             | string    | Link to the dashboard                                                                                                                                                                                               |

`defaultTimespan` object:

| Field            | Data Type | Notes                                                                                                               |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| timespanDuration | long      | Relative timespan in seconds. For example, `3600` (Last 1 hour).                                                    |
| timespanStart    | string    | Start of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-17 22:00:54`. |
| timespanEnd      | string    | End of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-19 22:00:54`.   |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboards.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Mon, 03 Sep 2019 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 225 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`[ { "dashboardId": "5e20da3b72fce8003257bcba", "title": "Dashboard Title A", "description": "Test Dashboard", "isBuiltIn": false, "accountId": 11, "createdBy": 6828, "modifiedBy": 6828, "modifiedDate": "2020-01-16 22:06:38", "isPrivate": false, "isDefaultForUser": false, "isDefaultForAccount": false, "defaultTimespan": { "timespanDuration": 86400 }, "globalOverride": false, "isMigratedReport": false, "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e20da3b72fce8003257bcba" }, ... ]`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`GET /v7/dashboards/{dashboardId}` Dashboard detail](broken-reference)

This endpoint returns a list of widgets configured in a ThousandEyes dashboard in addition to the dashboard’s metadata.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group. Specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{dashboardId}` the ID of the desired dashboard which can be found from the `/dashboards` endpoint.
* no request body

#### Response <a href="#response" id="response"></a>

Returns dashboard metadata information and associated widget list. Each widget will contain these properties in its configuration.

| Field Name          | Data Type | Notes                                                                                                                                                                                                               |
| ------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dashboardId         | string    | Unique ID of the dashboard                                                                                                                                                                                          |
| title               | string    | Title of the dashboard                                                                                                                                                                                              |
| createdBy           | integer   | ID of the user who created the dashboard, as returned by the `/v7/users` API endpoint                                                                                                                               |
| modifiedBy          | integer   | ID of the user who last modified the dashboard, as returned by the `/v7/users` API endpoint                                                                                                                         |
| modifiedDate        | string    | YYYY-MM-DD HH:mm:ss formatted date of last dashboard modification time, shown in UTC                                                                                                                                |
| description         | string    | A longer text explanation of what the dashboard does intended for the user. This field will be shown as text only. It may be used as help for other users but is not typically displayed when showing the dashboard |
| isBuiltIn           | boolean   | True for built-in reports, false for user-created reports                                                                                                                                                           |
| accountId           | integer   | ID of the account that the dashboard belongs to                                                                                                                                                                     |
| isPrivate           | boolean   | The dashboard can be viewed by other users in the account. If true, only the creator of the dashboard may view it. If false, all users in the same account may view it.                                             |
| isDefaultForUser    | boolean   | True if this dashboard is the default for the user, false otherwise                                                                                                                                                 |
| isDefaultForAccount | boolean   | True if this dashboard is the default for the account group, false otherwise                                                                                                                                        |
| defaultTimespan     | object    | Default timespan value to override widget timespans, see `defaultTimespan` below for details                                                                                                                        |
| globalOverride      | boolean   | True to override widget timespans and use defaultTimespan                                                                                                                                                           |
| isMigratedReport    | boolean   | True if this dashboard was previously a report                                                                                                                                                                      |
| widgets             | array     | An array of widget objects                                                                                                                                                                                          |
| apiLink             | string    | Link to the dashboard                                                                                                                                                                                               |

`defaultTimespan` object:

| Field            | Data Type | Notes                                                                                                               |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| timespanDuration | long      | Relative timespan in seconds. For example, `3600` (Last 1 hour).                                                    |
| timespanStart    | string    | Start of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-17 22:00:54`. |
| timespanEnd      | string    | End of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-19 22:00:54`.   |

The data returned for every widget will depend on the widget type. For Report widgets, refer to the Reports section of the documentation. Dashboard widgets will contain the following common properties:

| Field Name    | Data Type | Notes                                                                                                        |
| ------------- | --------- | ------------------------------------------------------------------------------------------------------------ |
| id            | string    | unique widget identifier inside the report. Note: Only unique within the same report, not across all reports |
| type          | string    | widget type: `Agent Status`, `Alert List`, `Color Grid`, `Test Table`                                        |
| visualMode    | string    | (optional, defaults to `Full`) Visual mode in the UI: `Full` or `Half screen`                                |
| fixedTimespan | object    | (optional) fixed timespan to do aggregation over. Specified with a value and unit (Days, Hours, or Minutes). |
| title         | string    | (optional, defaults to widget type string) widget title                                                      |
| isEmbedded    | boolean   | true if widget is marked as embedded, false otherwise                                                        |
| embedUrl      | string    | if widget is marked as embedded, `embedUrl` is provided                                                      |
| apiLink       | string    | link to the data of the widget                                                                               |

Each dashboard widget object will have some of these fields, depending on the widget type as they appear in the UI.

**Agent Status**

| Field Name | Data Type | Notes                                                        |
| ---------- | --------- | ------------------------------------------------------------ |
| agents     | string    | type of agent: `Enterprise` or `Endpoint`                    |
| show       | string    | ownership of agents: `Owned Agents` or `All Assigned Agents` |

**Alert List**

| Field Name   | Data Type | Notes                                                                              |
| ------------ | --------- | ---------------------------------------------------------------------------------- |
| alertTypes   | array     | list of alert types configured in the widget. An empty list means all alert types. |
| limitTo      | integer   | limit the number of alerts to be shown in the widget                               |
| activeWithin | object    | timespan during which alerts had to be active to be shown in the widget            |

**Color Grid**

| Field Name    | Data Type                | Notes                                                                                                                                                                                                                                                                                                     |
| ------------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataSource    | string                   | data source of widget. Can be `Alerts`, `Cloud & Enterprise Agents`, `Devices`, `Endpoint Agents`, etc.                                                                                                                                                                                                   |
| metricGroup   | string                   | metric group of widget as it appears in the UI. Can be `Web - HTTP Server`, `Voice - SIP Server`, `Network - Agent to Agent`, etc. Note: May not be required in some cases                                                                                                                                |
| metric        | string                   | metric of widget. Can be `Response Time`, `Total Error Count`, `Page Load Time`, `Marker Time`, `Packet Loss`, `Throughput`, etc.                                                                                                                                                                         |
| direction     | string                   | direction of agent to agent metric: `Source to Target`, `Target to Source`, or `Both Directions`. (Required for some metrics)                                                                                                                                                                             |
| measure       | object                   | measure configuration of the widget                                                                                                                                                                                                                                                                       |
| cards         | string                   | Property name to aggregate by. Can be `Tests`, `Test Labels`, `Continents`, `Countries`, etc.                                                                                                                                                                                                             |
| groupCardsBy  | string                   | Property name to group cards by. Can be `Tests`, `Test Labels`, `Continents`, `Countries`, etc.                                                                                                                                                                                                           |
| minScale      | float                    | (optional) minimum scale configured in the widget                                                                                                                                                                                                                                                         |
| maxScale      | float                    | (optional) maximum scale configured in the widget                                                                                                                                                                                                                                                         |
| unit          | string                   | (optional) Typically this is automatically configured. Possible options: `Kbps`, `Mbps`, `Gbps`, `Kpps`, `Mpps`, `Gpps`                                                                                                                                                                                   |
| columns       | integer                  | (optional) number of columns: 1 or 2                                                                                                                                                                                                                                                                      |
| limit         | integer                  | (optional) limit configured in the widget                                                                                                                                                                                                                                                                 |
| sortBy        | string                   | Property to sort by: `Value` or `Alphabetical`. Exception: Multi-metric table widget                                                                                                                                                                                                                      |
| sortDirection | string                   | Direction to sort by: `Ascending` or `Descending`                                                                                                                                                                                                                                                         |
| filters       | array of filter mappings | (optional) where the widget is filtered, filters property is shown. Each filter mapping will map a filter name to a list of filtered values. Filter keys can be `Agents`, `Agent Labels`, `Tests`, `Monitors`, etc. The list for each key holds the IDs of the property, i.e. `testId`s, `agentId`s, etc. |

**Test Table**

| Field Name | Data Type | Notes                                                                                                                         |
| ---------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| filter     | object    | multisearch filter (see below). Valid keys for filters: `Anything`, `Test Name`, `Target`, `Test ID`, `Test Type`, `Label ID` |
| exclude    | object    | multisearch filter (see below)                                                                                                |

**Multi Search Filter**

| Field Name | Data Type | Notes                                                                             |
| ---------- | --------- | --------------------------------------------------------------------------------- |
| filters    | list      | list of object pairs with a `key` and a `value` as shown in the app.              |
| type       | string    | string that defines the logical operator to be applied to filters: `all` or `any` |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboards/1.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Mon, 03 Sep 2019 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 232 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dashboardId": "5e1f7a99143ae6004fdc3bb4", "title": "Dashboard API", "description": "Test Dashboard", "isBuiltIn": false, "accountId": 11, "createdBy": 6103, "modifiedBy": 6103, "modifiedDate": "2020-01-16 21:09:09", "isPrivate": false, "isDefaultForUser": true, "isDefaultForAccount": false, "defaultTimespan": { "timespanDuration": 86400 }, "globalOverride": false, "isMigratedReport": false, "widgets": [ { "id": "xtzbr", "type": "Color Grid", "title": "Color Grid", "visualMode": "Full", "dataSource": "Cloud & Enterprise Agents", "metricGroup": "Web - HTTP Server", "metric": "Response Time", "measure": { "type": "Mean" }, "fixedTimespan": { "value": 1, "unit": "Hours" }, "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e1f7a99143ae6004fdc3bb4/xtzbr", "cards": "Tests", "groupCardsBy": "Agents", "columns": 1, "sortBy": "Value", "sortDirection": "Ascending" }, { "id": "vxqve", "type": "Agent Status", "title": "Agent Status", "visualMode": "Full", "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e1f7a99143ae6004fdc3bb4/vxqve", "agents": "Enterprise Agents", "show": "Owned Agents" }, { "id": "o6mjm", "type": "Test Table", "title": "Tests", "visualMode": "Full", "fixedTimespan": { "value": 12, "unit": "Hours" }, "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e1f7a99143ae6004fdc3bb4/o6mjm", "filter": { "filters": [ { "key": "Test Name", "value": "123" } ], "type": "all" }, "exclude": { "filters": [ { "key": "Label ID", "value": "25236" } ], "type": "all" } } ], "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e1f7a99143ae6004fdc3bb4" }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`GET /v7/dashboards/{dashboardId}/{widgetId}` Dashboard widget data](broken-reference)

This endpoint returns the raw data shown in a particular widget of a given dashboard.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.
* `rows={integer}` optional, the number of elements to receive per page. Only available for Alert List and Test Table Widget.
* `page={integer}` optional, specifies the page number for the data response. Only available in Test Table widget.
* `sortProperty={string}` optional, specifies the property to sort by. Only available for Alert List and Test Table Widget. See below for accepted values for each widget.
* `sortDirection={string}` optional, specifies the direction to sort by. Only available for Alert List and Test Table Widget. The possible values are `Ascending` or `Descending`. The default value is `Descending`.

#### Request <a href="#request" id="request"></a>

* `{dashboardId}` the ID of the dashboard you’re interested in.
* `{widgetId}` the ID of the widget for which to retrieve data.
* no request body

#### Response <a href="#response" id="response"></a>

Sends back a list of data elements associated with the dashboard. For Report widgets refer to the Reports page in the documentation. For Dashboard widgets, the data is returned with the following fields:

| Field Name  | Data Type                      | Notes                                                          |
| ----------- | ------------------------------ | -------------------------------------------------------------- |
| dateFrom    | dateTime                       | the start of the data shown in the API output                  |
| dateTo      | dateTime                       | end of the data window shown in the API output                 |
| binSize     | integer                        | duration of each bin (if applicable)                           |
| groupLabels | array of group labels          | see groupLabel fields below (if widget groups by any property) |
| data.points | array of data points           | see data point below                                           |
| data        | array of non-aggregated points | see below for Test Table, Alert List and Agent Status          |
| status      | string                         | Message for not fully configured widget or no data             |

The fields in **data.point** are the following:

| Field Name         | Data Type                         | Notes                                                            |
| ------------------ | --------------------------------- | ---------------------------------------------------------------- |
| timestamp          | integer                           | timestamp of the aggregated data point                           |
| numberOfDataPoints | integer                           | number of test data points aggregated into the widget data point |
| value              | float                             | aggregated value                                                 |
| groups             | array of group property and value | this corresponds to the groups used for the aggregation          |

The fields returned in **data** are dependent on the widget:

**Agent Status**

| Field Name | Data Type | Notes                                                                     |
| ---------- | --------- | ------------------------------------------------------------------------- |
| summary    | object    | object with a summary of how many agents are online, offline and disabled |
| agents     | array     | list of agents                                                            |

Each agent in the agent status data response will contain these properties

| Field Name | Data Type | Notes                                                                                            |
| ---------- | --------- | ------------------------------------------------------------------------------------------------ |
| agentId    | string    | ID of the agent                                                                                  |
| status     | string    | `ONLINE`, `OFFLINE` or `DISABLED`                                                                |
| ipInfo     | object    | information about the IP of the agent if `Enterprise` or operating system version for `Endpoint` |
| agentName  | string    | name of the agent                                                                                |
| location   | object    | contains the latitude, longitude and locationName of the agent                                   |

**Alert List**

This widget accepts the following query params to paginate the response:

* `rows={integer}` optional, the number of alerts in the response. The default value is the `limitBy` configured for the widget.
* `sortProperty={string}` optional, specifies the property to sort by. The possible values are `alertStatus` or `startTime`. The default value is `alertStatus`

| Field Name   | Data Type | Notes                                                                  |
| ------------ | --------- | ---------------------------------------------------------------------- |
| totalAlerts  | integer   | total number of alerts that were active within the timespan configured |
| activeAlerts | integer   | number of the alerts that are still active                             |
| alerts       | array     | array of alerts                                                        |

Each alert in the alert list data response will contain these properties

| Field Name        | Data Type | Notes                                                                                                 |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------- |
| active            | boolean   | `true` or `false`                                                                                     |
| alertId           | integer   | id of the alert                                                                                       |
| testId            | integer   | id of the test                                                                                        |
| sourceId          | integer   | id of the agent, monitor or device producing the alert                                                |
| sourceName        | string    | name of the agent, monitor or device producing the alert                                              |
| alertRule         | string    | name of the alert rule that this alert belongs to                                                     |
| alertType         | string    | name of the alert type                                                                                |
| startTime         | string    | date when the alert was first active                                                                  |
| durationInSeconds | integer   | number of seconds the alert was active. If it’s still active, this number will increase every second. |

**Test Table**

This widget accepts the following query params to paginate the response:

* `rows={integer}` optional, the number of alerts in the response. The default value is 10.
* `page={integer}` optional, specifies the page number for the data response. The default value is 1.
* `sortProperty={string}` optional, specifies the property to sort by. The possible values are `alertStatus`, `testName` or `testType`. The ordering may differ from the web application. The default value is `alertStatus`.

| Field Name | Data Type | Notes        |
| ---------- | --------- | ------------ |
| tests      | array     | list of test |

Each test in the test table data response will contain these properties

| Field Name  | Data Type | Notes                                                           |
| ----------- | --------- | --------------------------------------------------------------- |
| testId      | integer   | id of the test                                                  |
| testName    | string    | name of the test                                                |
| target      | string    | target configured in the test                                   |
| testType    | string    | type of test                                                    |
| alertStatus | integer   | number of active alerts for the test                            |
| isShared    | boolean   | flag set to true if the test has been shared                    |
| graphlets   | array     | list of timeseries points for test metrics in the last 12 hours |

Each graphlet object will contain these properties

| Field Name | Data Type | Notes                                                                                       |
| ---------- | --------- | ------------------------------------------------------------------------------------------- |
| metric     | string    | name of the metric                                                                          |
| testId     | integer   | id of the test                                                                              |
| points     | array     | list of `x` and `y` datapoints where `x` is the timestamp of the point and `y` is the value |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboards/2/vlvb1.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Mon, 02 Sep 2019 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 235 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

**Color Grid**

`{ "dateFrom": "2020-01-16 22:15:00", "dateTo": "2020-01-16 23:15:00", "groupLabels": [], "binSize": 300, "data": { "points": [ { "timestamp": 1579216200, "numberOfDataPoints": 3270, "value": 344.00582535755046, "groups": [ { "groupProperty": "Continents", "groupValue": "AS" } ] }, { "timestamp": 1579216200, "numberOfDataPoints": 5082, "value": 156.37737466049668, "groups": [ { "groupProperty": "Continents", "groupValue": "EU" } ] }, ... ] } }`

**Alert List**

`{ "dateFrom": "2020-01-16 22:28:52", "dateTo": "2020-01-16 23:28:52", "data": { "alertsData": { "totalAlerts": 590, "activeAlerts": 483, "alerts": [ { "alertId": 2004945, "testId": 56512, "ruleId": 281724, "alertSource": "AI Team Web Http Test 2", "alertRule": "AI dynamic baseline verification 11-21", "alertType": "Web - HTTP Server", "startTime": "2020-01-16 23:28:05", "durationInSeconds": 47, "active": true }, { "alertId": 2004941, "testId": 67035, "ruleId": 202156, "alertSource": "A2A uni CEA-13201 T10 Copy", "alertRule": "Delay always on", "alertType": "Network - Path Trace", "startTime": "2020-01-16 23:26:07", "durationInSeconds": 165, "active": true }, ... ] } } }`

**Test Table**

`{ "pages": { "next": "https://api.thousandeyes.com/v7/dashboards/5e2f669636256d0053617499/cogto?page=2" }, "dateFrom": "2020-01-30 17:04:10", "dateTo": "2020-01-31 05:04:10", "binSize": 300, "data": { "tests": [ { "testId": 68256, "testName": "$$$", "target": "https://www.google.com", "testType": "Web - HTTP Server", "alertStatus": 24, "isShared": true, "graphlets": [ { "metric": "Availability", "testId": 68256, "points": [ { "x": 1580403900, "y": 0.0 }, ... ] }, { "metric": "Response Time", "testId": 68256, "points": [ { "x": 1580406780, "y": 128.249 }, ... ] } ] }, ... ] } }`

**Agent Status**

`{ "dateTo": "2020-01-31 05:07:18", "binSize": 300, "data": { "summary": { "online": 10, "offline": 2, "disabled": 3 }, "agents": [ { "agentId": "6522", "status": "OFFLINE", "ipInfo": { "publicIp": "172.58.92.31", "privateIp": "172.17.0.3" }, "agentName": "0c3898000117", "location": { "latitude": 37.77493, "longitude": -122.41942, "locationName": "San Francisco, California, US" } }, ... ] } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`POST /v7/dashboards/create` Creating a dashboard](broken-reference)

This endpoint creates a new dashboard for the Login Account Group. User must have the `Edit dashboard templates for all users in account group` permission (Account Admin) or `Edit own dashboard templates` permission (Regular User) to create dashboards.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information.

#### Request <a href="#request" id="request"></a>

A Dashboard object with or without Widgets. See [Dashboard Detail](https://developer.thousandeyes.com/v7/#/dashboards-detail) for reference.

#### Response <a href="#response" id="response"></a>

Sends back the created dashboard configured in the current account group. Each dashboard contains the following fields:

| Field Name          | Data Type               | Notes                                                                                                                                                                                                                |
| ------------------- | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dashboardId         | string                  | Unique ID of the dashboard                                                                                                                                                                                           |
| title               | string                  | Title of the dashboard                                                                                                                                                                                               |
| isBuiltIn           | boolean                 | True for built-in dashboards, false for user-created dashboards                                                                                                                                                      |
| description         | string                  | A longer text explanation of what the dashboard does intended for the user. This field will be shown as text only. It may be used as help for other users but is not typically displayed when showing the dashboard. |
| accountId           | integer                 | ID of the account that the dashboard belongs to                                                                                                                                                                      |
| createdBy           | integer                 | ID of the user that created the dashboard                                                                                                                                                                            |
| modifiedDate        | dateTime                | The date/time when the dashboard was last modified                                                                                                                                                                   |
| isPrivate           | boolean                 | True if this dashboard is private                                                                                                                                                                                    |
| isDefaultForUser    | boolean                 | True if this dashboard is the default for the user, false otherwise                                                                                                                                                  |
| isDefaultForAccount | boolean                 | True if this dashboard is the default for the account group, false otherwise                                                                                                                                         |
| defaultTimespan     | object                  | Default timespan value to override widget timespans, see `defaultTimespan` below for details                                                                                                                         |
| globalOverride      | boolean                 | True to override widget timespans and use defaultTimespan                                                                                                                                                            |
| widgets             | array of widget objects | An array of widget objects                                                                                                                                                                                           |
| apiLink             | string                  | Link to the dashboard                                                                                                                                                                                                |

`defaultTimespan` can be relative or fixed with start and end. It can not be both. `defaultTimespan` object:

| Field            | Data Type | Notes                                                                                                               |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| timespanDuration | long      | Relative timespan in seconds. For example, `3600` (Last 1 hour).                                                    |
| timespanStart    | string    | Start of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-17 22:00:54`. |
| timespanEnd      | string    | End of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-19 22:00:54`.   |

The user can specify custom widget `id`s if they prefer to do so. These IDs have to match a 5 characters alphanumeric string and be unique across all widgets in the dashboard. Alternatively, the widget `id`s will be generated for them.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboards/create \ -d '{ "title": "HTTP Server Widgets" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Mon, 03 Sep 2019 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dashboardId": "5e1f7a99143ae6004fdc3bb4", "title": "HTTP Server Widgets", "description": "HTTP Server Widgets", "isBuiltIn": false, "accountId": 1, "createdBy": 1, "isPrivate": false, "isDefaultForUser": false, "isDefaultForAccount": false, "defaultTimespan": { "timespanDuration": "7200" }, "globalOverride": false, "widgets": [...], "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e1f7a99143ae6004fdc3bb4" }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`POST /v7/dashboards/{dashboardId}/update` Updating a dashboard](broken-reference)

This endpoint updates an existing dashboard for the account group that the user belongs to. Users with the `Edit dashboard templates for all users in account group` permission (Account Admin) can update any dashboard. Users with `Edit own dashboard templates` permission (Regular User) can only update the dashboards they have created.

* **Note:** This endpoint will do a **FULL** update, replacing the existing dashboard template with the object sent in the request. If a partial update is required, it’s recommended to first retrieve the dashboard, modify the dashboard object and then send it on the update.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group. Specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{dashboardId}` the ID of the dashboard you’re interested in.

A Dashboard object with or without Widgets.

#### Response <a href="#response" id="response"></a>

Sends back the updated dashboard. Each dashboard contains the following fields:

| Field Name          | Data Type               | Notes                                                                                        |
| ------------------- | ----------------------- | -------------------------------------------------------------------------------------------- |
| dashboardId         | string                  | Unique ID of the dashboard                                                                   |
| title               | string                  | Title of the dashboard                                                                       |
| description         | string                  | Description of the dashboard                                                                 |
| isBuiltIn           | boolean                 | True for built-in dashboards, false for user-created dashboards                              |
| accountId           | integer                 | ID of the account that the dashboard belongs to                                              |
| createdBy           | integer                 | ID of the user that created the dashboard                                                    |
| modifiedDate        | dateTime                | The date/time when the dashboard was last modified                                           |
| isPrivate           | boolean                 | True if this dashboard is private                                                            |
| isDefaultForUser    | boolean                 | True if this dashboard is the default for the user, false otherwise                          |
| isDefaultForAccount | boolean                 | True if this dashboard is the default for the account group, false otherwise                 |
| defaultTimespan     | object                  | Default timespan value to override widget timespans, see `defaultTimespan` below for details |
| globalOverride      | boolean                 | True to override widget timespans and use defaultTimespan                                    |
| widgets             | array of widget objects | An array of widget objects                                                                   |
| apiLink             | string                  | Link to the dashboard                                                                        |

`defaultTimespan` can be relative or fixed with start and end. It can not be both. `defaultTimespan` object:

| Field            | Data Type | Notes                                                                                                               |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| timespanDuration | long      | Relative timespan in seconds. For example, `3600` (Last 1 hour).                                                    |
| timespanStart    | string    | Start of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-17 22:00:54`. |
| timespanEnd      | string    | End of the timespan in UTC for timespan range in `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-19 22:00:54`.   |

The user can specify custom `widgetId`s if they prefer to do so. These IDs have to match a 5 characters alphanumeric string and be unique across all widgets in the dashboard. Alternatively, the `widgetId`s will be generated for them.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboards/1/update \ -d '{ "title": "New Dashboard Updated" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Mon, 03 Sep 2019 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 238 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`[ { "dashboardId": "5e1f7a99143ae6004fdc3bb4", "title": "HTTP Server Widgets", "description": "HTTP Server Widgets", "isBuiltIn": false, "accountId": 1, "createdBy": 1, "isPrivate": false, "isDefaultForUser": false, "isDefaultForAccount": false, "defaultTimespan": { "timespanDuration": "7200" }, "globalOverride": false, "widgets": [...], "apiLink": "https://api.thousandeyes.com/v7/dashboards/5e1f7a99143ae6004fdc3bb4" }, ... ]`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`POST /v7/dashboards/{dashboardId}/delete` Deleting a dashboard](broken-reference)

Deletes the specified dashboard in ThousandEyes, based on the dashboardId provided in the API request. Users with the `Edit dashboard templates for all users in account group` permission (Account Admin) can delete any dashboard. Users with `Edit own dashboard templates` permission (Regular User) can only delete the dashboards they have created.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{dashboardId}` the ID of the dashboard you would like to delete

#### Response <a href="#response" id="response"></a>

If the dashboard is successfully deleted, an HTTP 204 NO CONTENT response will be returned. If user lacks the permissions to delete the dashboard, an HTTP 401 UNAUTHORIZED response will be returned.

Response has no body.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl https://api.thousandeyes.com/v7/dashboards/1/delete \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Server: nginx Date: Mon, 03 Sep 2019 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1489585680 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`GET /v7/dasboard-snapshots` Dashboard snapshots list](broken-reference)

This endpoint returns a list of dashboard snapshots configured in ThousandEyes in the context of the user’s current account group. This endpoint requires the `View Snapshots` permission be assigned to the role of the user accessing this endpoint. Use this data to find a dashboard snapshot in your account, which is then used in other endpoint to access aggregated data.

#### Parameters <a href="#parameters" id="parameters"></a>

* `aid={aid}` Optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information
* `dashboardId={dashboardId}` Optional parameter to filter the list of snapshots by dashboard ID.

#### Request <a href="#request" id="request"></a>

* No request body.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboard-snapshots.json \ -u {email}:{authToken}`

`$ curl https://api.thousandeyes.com/v7/dashboard-snapshots.json\?dashboardId\=1 \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of dashboard snapshots configured in the current account group. The response has the following format:

| Field Name         | Data Type                           | Notes                                                        |
| ------------------ | ----------------------------------- | ------------------------------------------------------------ |
| pages              | page object                         | Object containing a pagination link to the next page: `next` |
| dashboardSnapshots | array of dashboard snapshot objects | See below                                                    |

Each dashboard snapshot object contains the following fields:

| Field Name         | Data Type                | Notes                                                          |
| ------------------ | ------------------------ | -------------------------------------------------------------- |
| snapshotId         | string                   | Unique ID of the dashboard snapshot                            |
| snapshotName       | string                   | Name of the dashboard snapshot                                 |
| createdDate        | dateTime                 | The date/time when dashboard snapshot was created              |
| isScheduled        | boolean                  | True if dashboard snapshot was generated from a schedule       |
| isShared           | boolean                  | True if dashboard snapshot is shared                           |
| accountId          | integer                  | ID of the account group that the snapshot belongs to           |
| timespan.startDate | dateTime                 | The date/time of beginning of dashboard snapshot               |
| timespan.duration  | integer                  | Duration of dashboard snapshot in seconds                      |
| permalink          | string                   | Link to dashboard snapshot in ThousandEyes Application         |
| apiLinks           | array of apiLink objects | A list of links which can be followed to pull more information |
| dashboard          | object                   | Dashboard upon which this dashboard snapshot is based upon.    |
| permalink          | string                   | Link to dashboard snapshot in ThousandEyes Application         |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 27 Jul 2022 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076340 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "pages": { "current": 1 }, "dashboardSnapshots": [ { "apiLinks": [...], "permalink": "https://api.thousandeyes.com/dashboard/?snapshotId=123", "createdDate": "2022-07-27 18:00:00", "dashboard": { "apiLinks": [...], "id": "1", "title": "Dashboard", "isBuiltIn": false, "accountId": 1, "createdBy": 2, "modifiedBy": 3, ... }, "isScheduled": true, "isShared": false, "snapshotId": "123", "accountId": 1, "snapshotName": "HTTP Server Dashboard Snapshot", "timeSpan": { "duration": 604800, "startDate": "2019-09-01 00:00:00" } }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`GET /v7/dashboard-snapshots/{snapshotId}` dashboard snapshot detail](broken-reference)

This endpoint returns a list of widgets configured in dashboard snapshot configured in ThousandEyes. Seed this endpoint with a snapshotId found from the /dashboard-snapshots endpoint. This endpoint requires the `View Snapshots` permission be assigned to the role of the user accessing this endpoint.

#### Parameters <a href="#parameters" id="parameters"></a>

* `aid={aid}` Optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information
* `{snapshotId}` The ID of the dashboard snapshot you’re interested in.

#### Request <a href="#request" id="request"></a>

* No request body.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboard-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns details information about dashboard snapshot including the list and configuration of the widgets.

| Field Name         | Data Type                | Notes                                                            |
| ------------------ | ------------------------ | ---------------------------------------------------------------- |
| snapshotId         | string                   | Unique ID of the dashboard snapshot                              |
| snapshotName       | string                   | Name of the dashboard snapshot                                   |
| createdDate        | dateTime                 | The date/time when dashboard snapshot was created                |
| isScheduled        | boolean                  | True if dashboard snapshot was generated from a schedule         |
| isShared           | boolean                  | True if dashboard snapshot is shared                             |
| accountId          | integer                  | ID of the account group that the snapshot belongs to             |
| timespan.startDate | dateTime                 | The date/time of beginning of dashboard snapshot                 |
| timespan.duration  | integer                  | Duration of dashboard snapshot in seconds                        |
| permalink          | string                   | Link to dashboard snapshot in ThousandEyes Application           |
| apiLinks           | array of apiLink objects | A list of links which can be followed to pull more information   |
| dashboard          | object                   | Dashboard this dashboard snapshot is based upon.                 |
| widgets            | object                   | Widgets in the snapshot. Refer to the Widget object description. |
| permalink          | string                   | Link to dashboard snapshot in ThousandEyes Application           |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 27 Jul 2022 09:41:13 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "apiLinks": [...], "createdDate": "2022-07-27 14:42:49", "permalink": "https://app.thousandeyes.com/dashboard/?snapshotId=60886ebb-2466-444d-bbd8-74d5ea1402d2", "dashboard": { "apiLinks": [...], "builtIn": 1, "id": "2", "name": "ThousandEyes Built-in" }, "scheduled": 0, "shared": 0, "snapshotId": "60886ebb-2466-444d-bbd8-74d5ea1402d2", "snapshotName": "Dashboard Snapshot", "timeSpan": { "duration": 604800, "startDate": "2022-07-23 00:00:00" }, "widgets": [ { "id": "abcd1", "type": "Multi Metric Table", "title": "Multi Metric Table", "visualMode": "Full", "apiLink": "https://api.thousandeyes.com/v7/dashboard-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2/abcd1", "rowGroupBy": "Devices", "sortBy": "Default (Devices)", "sortDirection": "Ascending", "multiMetricColumns": [ { "id": "abcd2", "dataSource": "Devices", "metric": "Availability", "measure": { "type": "% Active" } }, { "id": "abcd3", "dataSource": "Devices", "metric": "Availability", "measure": { "type": "% Inactive" } } ] }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`GET /v7/dashboard-snapshots/{snapshotId}/{widgetId}` Dashboard snapshot data](broken-reference)

This endpoint returns actual metrics used in the generation of the dashboard snapshot shown.

#### Parameters <a href="#parameters" id="parameters"></a>

* `aid={aid}` Optional. Changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.
* `{snapshotId}` The ID of the dashboard snapshot you’re interested in.
* `{widgetId}` The ID of the widget for which to retrieve data.

#### Request <a href="#request" id="request"></a>

* No request body.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboard-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2/1234f.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back a list of data elements associated with the dashboard snapshot. The data components are aggregated by our services, then reported back in bins: each bin represents a point on the chart: the granularity of the points shown in the chart is based on the data range shown in the dashboard snapshot. Bin sizes are based on the table below:

| Dashboard time range | Bin size  |
| -------------------- | --------- |
| up to 1 day          | 5 minutes |
| 1 day - 14 days      | 1 hour    |
| 15 days - 30 days    | 2 hours   |
| 31 days - 50 days    | 4 hours   |
| 51 days - 93 days    | 6 hours   |

If your data is grouped, a value will be shown for each data grouping for each bin.

Corresponding data is returned according to the format for widget data. Check the endpoint to return widget data for reference.

`HTTP/1.1 200 OK Server: nginx Date: Wed, 27 Jul 2022 14:29:51 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1492093800 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dateFrom": "2022-07-24 16:00:00", "dateTo": "2022-07-25 16:00:00", "groupLabels": [ { "groupProperty": "Countries", "groupLabels": [ { "groupId": "DE", "groupLabel": "Germany" }, { "groupId": "AU", "groupLabel": "Australia" }, ... ] } ], "binSize": 3600, "data": { "points": [ { "timestamp": 1563984000, "numberOfDataPoints": 62, "value": 569.0499070690524, "groups": [ { "groupProperty": "Countries", "groupValue": "AU" } ] }, ... ] } }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`POST /v7/dashboard-snapshots/create` Creating a dashboard snapshot](broken-reference)

This endpoint creates a new dashboard snapshot for the account group that the user belongs to. This endpoint requires the `Edit Snapshots` permission be assigned to the role of the user accessing this endpoint.

#### Parameters <a href="#parameters" id="parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

The endpoint expects a JSON object with the following fields:

| Field Name  | Data Type | Notes                                                 |
| ----------- | --------- | ----------------------------------------------------- |
| displayName | string    | The name of the snapshot. Does not have to be unique. |
| from        | dateTime  | The date and time to start aggregating data           |
| to          | string    | The date and time to end aggregating data             |
| dashboardId | string    | The ID of the dashboard to generate a snapshot from   |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v7/dashboard-snapshots/create \ -d '{ "displayName": "snapshot from API", "from": "2022-07-26 18:00:00", "to": "2022-07-26 19:00:00", "dashboardId": "123" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back the id of the created dashboard snapshot:

| Field Name | Data Type | Notes                                                       |
| ---------- | --------- | ----------------------------------------------------------- |
| snapshotId | string    | Unique ID of the dashboard snapshot that is being generated |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 27 Jul 2022 18:00:00 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076340 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "snapshotId": "1234" }` For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).

[`POST /v7/dashboard-snapshots/{snapshotId}/delete` Deleting a dashboard snapshot](broken-reference)

Deletes the specified dashboard snapshot in ThousandEyes, based on the snapshotId provided in the API request. Users with the `Edit reports for all users in account group` permission (Account Admin) can delete any dashboard snapshot.

#### Parameters <a href="#parameters" id="parameters"></a>

* `aid={aid}` Optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v7/#/accountcontext) for more information
* `{snapshotId}` The ID of the dashboard snapshot you would like to delete

#### Response <a href="#response" id="response"></a>

If the dashboard snapshot is successfully deleted, an HTTP 204 NO CONTENT response will be returned. If user lacks the permissions to delete the dashboard snapshot, an HTTP 401 UNAUTHORIZED response will be returned.

Response has no body.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl https://api.thousandeyes.com/v7/dashboard-snapshots/2bee381c-cc97-49f4-9ef5-1013c97f4124/delete \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Server: nginx Date: Wed, 27 Jul 2022 09:43:28 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v7/#/statuscodes).
