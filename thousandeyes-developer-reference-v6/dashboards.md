# Dashboards

### Dashboards

[`GET /v6/dashboards` Dashboards list](broken-reference)

This endpoint returns a list of dashboards configured in ThousandEyes in the context of the user’s current account group. Use this data to find a dashboard in your account, which is then used in other endpoints to access aggregated data.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dashboards.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of dashboards configured in the current account group. Each dashboard contains the following fields:

| Field Name          | Data Type                | Notes                                                                                                                                                                                                                |
| ------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                  | string                   | unique ID of the dashboard                                                                                                                                                                                           |
| name                | string                   | title of the dashboard                                                                                                                                                                                               |
| description         | string                   | A longer text explanation of what the dashboard does intended for the user. This field will be shown as text only. It may be used as help for other users but is not typically displayed when showing the dashboard. |
| isBuiltIn           | boolean                  | true for built-in dashboards, false for user-created dashboards                                                                                                                                                      |
| createdBy           | integer                  | ID of the user that created the dashboard                                                                                                                                                                            |
| modifiedBy          | integer                  | ID of the user that last modified the dashboard                                                                                                                                                                      |
| modifiedDate        | dateTime                 | the date/time when the dashboard was last modified                                                                                                                                                                   |
| accountId           | integer                  | ID of the account that the dashboard belongs to                                                                                                                                                                      |
| isPrivate           | boolean                  | The dashboard can be viewed by other users in the account. If true, only the creator of the dashboard may view it. If false, all users in the same account may view it.                                              |
| isDefaultForUser    | boolean                  | True if this dashboard is the default for the user; false otherwise                                                                                                                                                  |
| isDefaultForAccount | boolean                  | True if this dashboard is the default for the account group; false otherwise                                                                                                                                         |
| defaultTimespan     | object                   | Default timespan value to override widget timespans. See `defaultTimespan` below for details.                                                                                                                        |
| globalOverride      | boolean                  | True to override widget timespans and use defaultTimespan                                                                                                                                                            |
| isMigratedReport    | boolean                  | True if this dashboard was previously a report                                                                                                                                                                       |
| apiLinks            | array of apiLink objects | A list of links which can be followed to pull more information                                                                                                                                                       |

`defaultTimespan` object:

| Field            | Data Type | Notes                                                                                                                   |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------- |
| timespanDuration | long      | Relative timespan in seconds. For example, `3600` (Last 1 hour).                                                        |
| timespanStart    | string    | Start of the timespan, in UTC, for timespan range. Use `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-17 22:00:54`. |
| timespanEnd      | string    | End of the timespan, in UTC, for timespan range. Use `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-19 22:00:54`.   |

`HTTP/1.1 200 OK Server: nginx Date: Tue, 01 Mar 2022 17:53:57 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dashboards": [ { "id": "620ecb8e0112131fa51e263e", "name": "Dashboard Title A", "description": "Test Dashboard", "isBuiltIn": false, "createdBy": 6699, "modifiedBy": 6699, "modifiedDate": "2022-02-22 18:10:04", "accountId": 11, "isPrivate": false, "isDefaultForUser": false, "isDefaultForAccount": false, "defaultTimespan": { "timespanDuration": 86400 }, "globalOverride": false, "isMigratedReport": false, "apiLinks": [...] }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dashboards/{dashboardId}` Dashboards detail](broken-reference)

This endpoint returns a list of widgets configured in dashboards configured in ThousandEyes. Seed this endpoint with an id found from the /dashboards endpoint.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{dashboardId}` the ID of the dashboard you’re interested in.

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dashboards/620b1511048612499a42ac98.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns dashboard metadata information and associated widget list. Each widget will contain these properties in its configuration.

| Field Name          | Data Type                | Notes                                                                                                                                                                                                                |
| ------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                  | string                   | unique ID of the dashboard                                                                                                                                                                                           |
| name                | string                   | title of the dashboard                                                                                                                                                                                               |
| description         | string                   | A longer text explanation of what the dashboard does intended for the user. This field will be shown as text only. It may be used as help for other users but is not typically displayed when showing the dashboard. |
| isBuiltIn           | boolean                  | true for built-in dashboards, false for user-created dashboards                                                                                                                                                      |
| createdBy           | integer                  | ID of the user who created the dashboard, as returned by the `/v6/users` API endpoint                                                                                                                                |
| modifiedBy          | integer                  | ID of the user who last modified the dashboard, as returned by the `/v6/users` API endpoint                                                                                                                          |
| modifiedDate        | string                   | YYYY-MM-DD HH:mm:ss formatted date of last dashboard modification time, shown in UTC                                                                                                                                 |
| accountId           | integer                  | ID of the account that the dashboard belongs to                                                                                                                                                                      |
| isPrivate           | boolean                  | The dashboard can be viewed by other users in the account. If true, only the creator of the dashboard may view it. If false, all users in the same account may view it.                                              |
| isDefaultForUser    | boolean                  | True if this dashboard is the default for the user; false otherwise                                                                                                                                                  |
| isDefaultForAccount | boolean                  | True if this dashboard is the default for the account group; false otherwise                                                                                                                                         |
| defaultTimespan     | object                   | Default timespan value to override widget timespans. See `defaultTimespan` below for details                                                                                                                         |
| globalOverride      | boolean                  | Set to true in order to override widget timespans and use defaultTimespan                                                                                                                                            |
| isMigratedReport    | boolean                  | True if this dashboard was previously a report                                                                                                                                                                       |
| apiLinks            | array of apiLink objects | a list of links which can be followed to pull more information                                                                                                                                                       |
| widgets             | array                    | an array of widget objects                                                                                                                                                                                           |

`defaultTimespan` object:

| Field            | Data Type | Notes                                                                                                                   |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------- |
| timespanDuration | long      | Relative timespan in seconds. For example, `3600` (Last 1 hour).                                                        |
| timespanStart    | string    | Start of the timespan, in UTC, for timespan range. Use `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-17 22:00:54`. |
| timespanEnd      | string    | End of the timespan, in UTC, for timespan range. Use `yyyy-MM-dd HH:mm:ss` format. For example `2022-07-19 22:00:54`.   |

The data returned for every widget will depend on the widget type. For Report widgets, refer to the Reports section of the documentation. Dashboard widgets will contain the following common properties:

| Field Name     | Data Type | Notes                                                   |
| -------------- | --------- | ------------------------------------------------------- |
| title          | string    | widget title                                            |
| type           | string    | widget type; `Agent Status`, `Alert List`, `Test Table` |
| dataComponents | array     | array of widget data components                         |
| embedUrl       | string    | if widget is marked as embedded, embedUrl is provided   |

Each dashboard widget is comprised of one or more data components, common fields represented by the following table:

| Field Name      | Data Type                | Notes                                                                             |
| --------------- | ------------------------ | --------------------------------------------------------------------------------- |
| dataComponentId | string                   | unique ID of the data component. Use this value to retrieve dataComponent values. |
| apiLinks        | array of apiLink objects | a list of links which can be followed to pull more information                    |

Each dashboard widget object will have some of these fields, depending on the widget type as they appear in the UI.

**Agent Status**

| Field Name | Data Type                | Notes                                                                                                                                                                                                                                                                                            |
| ---------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| agents     | string                   | type of agent: `Enterprise` or `Endpoint`                                                                                                                                                                                                                                                        |
| show       | string                   | ownership of agents: `Owned Agents` or `All Assigned Agents`                                                                                                                                                                                                                                     |
| filters    | array of filter mappings | (optional) where the widget is filtered, filters property is shown. Each filter mapping will map a filter name to a list of filtered values. Filter properties can be `Agents`, `Agent Labels`, etc. The list for each key holds the IDs of the property, i.e. `agentId`s, `agentLabelId`s, etc. |

**Alert List**

| Field Name   | Data Type                | Notes                                                                                                                                                                                                                                                                                                               |
| ------------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alertTypes   | array                    | list of alert types configured in the widget. An empty list means all alert types.                                                                                                                                                                                                                                  |
| limitTo      | integer                  | limit the number of alerts to be shown in the widget                                                                                                                                                                                                                                                                |
| activeWithin | object                   | timespan during which alerts had to be active to be shown in the widget                                                                                                                                                                                                                                             |
| filters      | array of filter mappings | (optional) where the widget is filtered, filters property is shown. Each filter mapping will map a filter name to a list of filtered values. Filter properties can be `Alert Rules`, `Monitors`, `Tests`, `Test Labels`, etc. The list for each key holds the IDs of the property, i.e. `agentId`s, `testId`s, etc. |

**Test Table**

| Field Name                           | Data Type | Notes                                                                                                                         |
| ------------------------------------ | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| filter                               | object    | multisearch filter (see below). Valid keys for filters: `Anything`, `Test Name`, `Target`, `Test ID`, `Test Type`, `Label ID` |
| exclude                              | object    | multisearch filter (see below)                                                                                                |
| shouldExcludeAlertSuppressionWindows | boolean   | true for excluding alert suppression windows                                                                                  |

**Multi Search Filter**

| Field Name | Data Type | Notes                                                                             |
| ---------- | --------- | --------------------------------------------------------------------------------- |
| filters    | list      | list of object pairs with a `key` and a `value` as shown in the app.              |
| type       | string    | string that defines the logical operator to be applied to filters: `all` or `any` |

`HTTP/1.1 200 OK Server: nginx Date: Tue, 01 Mar 2022 22:50:32 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dashboards": [ { "id": "620b1511048612499a42ac98", "name": "Dashboard Demo A", "description": "Test Dashboard", "isBuiltIn": false, "createdBy": 6825, "modifiedBy": 6825, "modifiedDate": "2022-03-01 22:31:30", "accountId": 11, "isPrivate": false, "isDefaultForUser": false, "isDefaultForAccount": false, "defaultTimespan": { "timespanDuration": 86400 }, "globalOverride": false, "isMigratedReport": false, "widgets": [ { "type": "Agent Status", "title": "Agent Status", "dataComponents": [ { "dataComponentId": "ayear", "filters": [ { "filterProperty": "Agents", "filterValue": "11119789" }, { "filterProperty": "Agents", "filterValue": "6522" }, { "filterProperty": "Agents", "filterValue": "6381" } ], "apiLinks": [...], "agents": "Enterprise Agents", "show": "Owned Agents" } ] }, { "type": "Tests", "title": "Tests", "dataComponents": [ { "dataComponentId": "vug1s", "apiLinks": [...], "shouldExcludeAlertSuppressionWindows": false, "filter": { "filters": [ { "value": "test", "key": "Anything" } ], "type": "all" }, "exclude": { "filters": [ { "value": "Some String", "key": "Test Name" } ], "type": "all" } } ] }, { "type": "Alert List", "title": "Alert List", "dataComponents": [ { "dataComponentId": "wvcii", "apiLinks": [...], "alertTypes": [ "Routing - BGP" ], "limitTo": 10, "activeWithin": { "value": 1, "unit": "Hours" } } ] }, ], "apiLinks": [...] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dashboards/{dashboardId}/{dataComponentId}` Dashboard data](broken-reference)

This endpoint returns the raw data shown in a particular widget of a given dashboard.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.
* `{dashboardId}` the ID of the dashboard you’re interested in.
* `{dataComponentId}` the ID of the data component for which to retrieve data.

#### Request <a href="#request" id="request"></a>

* no request body

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dashboards/2/vlvb1.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back a list of data elements associated with the dashboard. For Report widgets refer to the Reports page in the documentation. For Dashboard widgets, the data is returned with the following fields:

| Field Name        | Data Type                      | Notes                                                 |
| ----------------- | ------------------------------ | ----------------------------------------------------- |
| from              | dateTime                       | the start of the data shown in the API output         |
| to                | dateTime                       | end of the data window shown in the API output        |
| dataComponentData | array of non-aggregated points | see below for Test Table, Alert List and Agent Status |

The fields returned in **dataComponentData** are dependent on the widget:

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

`HTTP/1.1 200 OK Server: nginx Date: Wed, 02 Mar 2022 00:00:10 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

**Agent Status**

`{ "to": "2022-03-02 00:04:48", "reportDataComponentData": { "summary": { "online": 0, "offline": 2, "disabled": 1 }, "agents": [ { "agentId": "6522", "status": "OFFLINE", "ipInfo": { "publicIp": "172.58.92.31", "privateIp": "172.17.0.3" }, "agentName": "0c3898000117", "location": { "latitude": 37.77493, "longitude": -122.41942, "locationName": "San Francisco, California, US" } }, ... ] } }`

**Alert List**

`{ "from": "2022-03-01 23:09:21", "to": "2022-03-02 00:09:21", "reportDataComponentData": { "totalAlerts": 2539, "activeAlerts": 2334, "alerts": [ { "alertType": "Routing - BGP", "active": true, "isActive": true, "alertId": 6394171, "testId": 123266, "ruleId": 250, "alertSource": "BGP-Test", "alertRule": "Default BGP Alert Rule", "startTime": "2022-03-01 22:15:00", "durationInSeconds": 6861 }, ... ] } }`

**Test Table**

`{ "from": "2022-03-01 12:14:45", "to": "2022-03-02 00:14:45", "pages": { "next": "https://api.thousandeyes.com/v6/dashboards/620b1511048612499a42ac98/vug1s.json?pageId=2", "current": 1 }, "reportDataComponentData": { "tests": [ { "graphlets": [ { "points": [ { "x": 1646136000, "y": 0 }, ... ], "metric": "Path Changes", "testId": 123419 }, { "points": [ { "x": 1646136000, "y": 95.83333333333334 }, ... ], "metric": "Reachability", "testId": 123419 } ], "testId": 123419, "testName": "Bgp test 08/19/2020 only public monitors - 4", "target": "64.233.160.0/19", "testType": "Routing - BGP", "alertStatus": 296, "isShared": false }, ... ] } }` For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/dashboards/{dashboardId}/delete` Deleting a dashboard](broken-reference)

Deletes the specified dashboard in ThousandEyes, based on the dashboardId provided in the API request. Users with the `Edit dashboard templates for all users in account group` permission (Account Admin) can delete any dashboard. Users with `Edit own dashboard templates` permission (Regular User) can only delete the dashboards they have created.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{dashboardId}` the ID of the dashboard you would like to delete

#### Response <a href="#response" id="response"></a>

If the dashboard is successfully deleted, an HTTP 204 NO CONTENT response will be returned. If user lacks the permissions to delete the dashboard, an HTTP 401 UNAUTHORIZED response will be returned.

Response has no body.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/dashboards/58c9437149b02d5410fd06cd/delete.json \ -d '' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Server: nginx Date: Tue, 01 Mar 2022 22:50:32 GMT Content-Type: application/json;charset=UTF-8 Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1489585680 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dashboard-snapshots` Dashboard snapshots list](broken-reference)

This endpoint returns a list of dashboard snapshots configured in ThousandEyes in the context of the user’s current account group. This endpoint requires the `View snapshots` permission be assigned to the role of the user accessing this endpoint. Use this data to find a dashboard snapshot in your account, which is then used in other endpoint to access aggregated data.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` Optional. Specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information.
* `aid={aid}` Optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* No request body.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dashboard-snapshots.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of dashboard snapshots configured in the current account group. Each dashboard snapshot object contains the following fields:

| Field Name         | Data Type                | Notes                                                          |
| ------------------ | ------------------------ | -------------------------------------------------------------- |
| snapshotId         | string                   | unique ID of the dashboard snapshot                            |
| snapshotName       | string                   | name of the dashboard snapshot                                 |
| createdDate        | dateTime                 | the date/time when dashboard snapshot was created              |
| scheduled          | boolean                  | 1 if dashboard snapshot was generated from a schedule          |
| shared             | boolean                  | 1 if dashboard snapshot is shared                              |
| dashboard          | object                   | dashboard this dashboard snapshot is based upon.               |
| timespan.startDate | dateTime                 | the date/time of beginning of dashboard snapshot               |
| timespan.duration  | integer                  | duration of dashboard snapshot in seconds                      |
| permalink          | string                   | link to dashboard snapshot in ThousandEyes Application         |
| apiLinks           | array of apiLink objects | a list of links which can be followed to pull more information |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 27 Jul 2022 09:38:58 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076340 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "pages": { "current": 1 }, "dashboardSnapshots": [ { "apiLinks": [...], "createdDate": "2022-07-27 14:42:49", "permalink": "https://app.thousandeyes.com/dashboard/?snapshotId=60886ebb-2466-444d-bbd8-74d5ea1402d2", "dashboard": { "apiLinks": [...], "builtIn": 1, "id": "0", "name": "ThousandEyes Built-in" }, "scheduled": 0, "shared": 0, "snapshotId": "60886ebb-2466-444d-bbd8-74d5ea1402d2", "snapshotName": "Dashboard Snapshot", "timeSpan": { "duration": 604800, "startDate": "2022-07-01 00:00:00" } }, ... ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dashboard-snapshots/{snapshotId}` Dashboards snapshot detail](broken-reference)

This endpoint returns a list of widgets configured in dashboard snapshot configured in ThousandEyes. Seed this endpoint with a snapshotId found from the /dashboard-snapshots endpoint. This endpoint requires the `View Snapshots` permission be assigned to the role of the user accessing this endpoint.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` Optional. Specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information.
* `aid={aid}` Optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{snapshotId}` The ID of the dashboard snapshot you’re interested in.

#### Request <a href="#request" id="request"></a>

* No request body.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dashboard-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Returns details information about dashboard snapshot including the list and configuration of the widgets.

| Field Name         | Data Type                | Notes                                                          |
| ------------------ | ------------------------ | -------------------------------------------------------------- |
| snapshotId         | string                   | Unique ID of the dashboard snapshot                            |
| snapshotName       | string                   | Name of the dashboard snapshot                                 |
| createdDate        | dateTime                 | The date/time when dashboard snapshot was created              |
| scheduled          | boolean                  | 1 if dashboard snapshot was generated from a schedule          |
| shared             | boolean                  | 1 if dashboard snapshot is shared                              |
| dashboard          | object                   | Dashboard upon which this dashboard snapshot is based.         |
| timespan.startDate | dateTime                 | The date/time of beginning of dashboard snapshot               |
| timespan.duration  | integer                  | Duration of dashboard snapshot in seconds                      |
| permalink          | string                   | Link to dashboard snapshot in ThousandEyes Application         |
| apiLinks           | array of apiLink objects | A list of links which can be followed to pull more information |
| widgets            | array                    | An array of widget objects                                     |

Sends back a list of data elements associated with the dashboard snapshot. For Report widgets refer to the Reports page in the documentation. For Dashboard widgets, the data is returned with the following fields:

| Field Name     | Data Type | Notes                                                   |
| -------------- | --------- | ------------------------------------------------------- |
| title          | string    | Widget title                                            |
| type           | string    | Widget type; `Agent Status`, `Alert List`, `Test Table` |
| dataComponents | array     | Array of widget data components                         |
| embedUrl       | string    | If widget is marked as embedded, embedUrl is provided   |

Each dashboard widget is comprised of one or more data components, common fields represented by the following table:

| Field Name      | Data Type                | Notes                                                                             |
| --------------- | ------------------------ | --------------------------------------------------------------------------------- |
| dataComponentId | string                   | Unique ID of the data component. Use this value to retrieve dataComponent values. |
| apiLinks        | array of apiLink objects | A list of links which can be followed to pull more information                    |

Each dashboard-snapshot widget object will have some of these fields, depending on the widget type as they appear in the UI.

**Agent Status**

| Field Name | Data Type                | Notes                                                                                                                                                                                                                                                                                                 |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agents     | string                   | Type of agent: `Enterprise` or `Endpoint`                                                                                                                                                                                                                                                             |
| show       | string                   | Ownership of agents: `Owned Agents` or `All Assigned Agents`                                                                                                                                                                                                                                          |
| filters    | array of filter mappings | (optional) Where the widget is filtered, the filter’s property is shown. Each filter mapping will map a filter name to a list of filtered values. Filter properties can be `Agents`, `Agent Labels`, etc. The list for each key holds the IDs of the property, i.e. `agentId`s, `agentLabelId`s, etc. |

**Alert List**

| Field Name   | Data Type                | Notes                                                                                                                                                                                                                                                                                                                    |
| ------------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| alertTypes   | array                    | List of alert types configured in the widget. An empty list means all alert types.                                                                                                                                                                                                                                       |
| limitTo      | integer                  | Limit the number of alerts to be shown in the widget                                                                                                                                                                                                                                                                     |
| activeWithin | object                   | Timespan during which alerts had to be active to be shown in the widget                                                                                                                                                                                                                                                  |
| filters      | array of filter mappings | (optional) Where the widget is filtered, the filter’s property is shown. Each filter mapping will map a filter name to a list of filtered values. Filter properties can be `Alert Rules`, `Monitors`, `Tests`, `Test Labels`, etc. The list for each key holds the IDs of the property, i.e. `agentId`s, `testId`s, etc. |

**Test Table**

| Field Name                           | Data Type | Notes                                                                                                                         |
| ------------------------------------ | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| filter                               | object    | Multisearch filter (see below). Valid keys for filters: `Anything`, `Test Name`, `Target`, `Test ID`, `Test Type`, `Label ID` |
| exclude                              | object    | Multisearch filter (see below)                                                                                                |
| shouldExcludeAlertSuppressionWindows | boolean   | True for excluding alert suppression windows                                                                                  |

**Multi Search Filter**

| Field Name | Data Type | Notes                                                                             |
| ---------- | --------- | --------------------------------------------------------------------------------- |
| filters    | list      | List of object pairs with a `key` and a `value` as shown in the app.              |
| type       | string    | String that defines the logical operator to be applied to filters: `all` or `any` |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 22 Jul 2022 09:41:13 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "dashboardSnapshots": [ { "apiLinks": [...], "createdDate": "2022-07-27 14:42:49", "permalink": "https://app.thousandeyes.com/dashboard/?snapshotId=60886ebb-2466-444d-bbd8-74d5ea1402d2", "dashboard": { "apiLinks": [...], "builtIn": 1, "id": "2", "name": "ThousandEyes Built-in" }, "scheduled": 0, "shared": 0, "snapshotId": "60886ebb-2466-444d-bbd8-74d5ea1402d2", "snapshotName": "Dashboard Snapshot", "timeSpan": { "duration": 604800, "startDate": "2022-07-01 00:00:00" }, "widgets": [ { "dataComponents": [ { "apiLinks": [...], "dataComponentId": "59089917755cb04ee9944e44", "description": "Average Availability", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Availability" }, { "apiLinks": [...], "dataComponentId": "59089ae6755cb04ee977703b", "description": "Average Response Time", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Response Time" }, ... ], "title": "HTTP Server Overview", "type": "numbers" }, { "dataComponents": [ { "apiLinks": [...], "dataComponentId": "590897e4755cb04ee9776f5b", "groupBy": [], "measure": "Mean", "metric": "Web - HTTP Server \u2014 Availability" } ], "title": "Overall Average Availability", "type": "timeseries" }, ... ] } ] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/dashboard-snapshots/{snapshotId}/{dataComponentId}` Dashboard snapshot data](broken-reference)

This endpoint returns actual metrics used in the generation of the dashboard snapshot shown.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` Optional. Specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information.
* `aid={aid}` Optional. Changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.
* `{snapshotId}` The ID of the dashboard snapshot you’re interested in.
* `{dataComponentId}` The ID of the data component for which to retrieve data.

#### Request <a href="#request" id="request"></a>

* No request body.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/dashboard-snapshots/60886ebb-2466-444d-bbd8-74d5ea1402d2/59089917755cb04ee9944e44.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back a list of data elements associated with the dashboard snapshot. The data components are aggregated by our services, then reported back in bins. Each bin represents a point on the chart. The granularity of the points shown on the chart is based on the data range shown in the dashboard snapshot. Bin sizes are based on the table below:

| Dashboard time range | Bin size  |
| -------------------- | --------- |
| up to 1 day          | 5 minutes |
| 1 day - 14 days      | 1 hour    |
| 15 days - 30 days    | 2 hours   |
| 31 days - 50 days    | 4 hours   |
| 50 days - 93 days    | 6 hours   |

If your data is grouped, a value will be shown for each data grouping for each bin. Corresponding data is returned according to the following fields:

| Field Name              | Data Type | Notes                                                           |
| ----------------------- | --------- | --------------------------------------------------------------- |
| from                    | dateTime  | Start date of the timespan for the data shown in the API output |
| to                      | dateTime  | End date of the timespan for the data shown in the API output   |
| reportDataComponentData | object    | object represents dashboard widget data                         |

`reportDataComponentData` object has the following fields for dashboard widgets:

| Field Name                  | Data Type                      | Notes                                                                                                                                               |
| --------------------------- | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| data.binId                  | integer                        | Corresponds to the start time for the bin                                                                                                           |
| data.count                  | integer                        | Number of datapoints shown in the round                                                                                                             |
| data.value                  | float                          | Value of the datapoint                                                                                                                              |
| data.groups                 | array of group objects         | This corresponds to how the data is labelled in the widget. Match the groupProperty and groupId to retrieve the label as represented in the widget. |
| groupLabelMaps              | array of groupLabelMap objects | See groupLabelMap fields below                                                                                                                      |
| groupLabelMap.groupProperty | string                         | Matches the groupProperty listed in the data.groups object                                                                                          |
| groupLabelMap.groupLabels   | array of groupLabel objects    | See individual fields below                                                                                                                         |
| groupLabel.groupId          | integer                        | Lookup value of the group                                                                                                                           |
| groupLabel.groupLabel       | string                         | Value of the legend                                                                                                                                 |
| binSize                     | integer                        | Duration of each bin                                                                                                                                |

`reportDataComponentData` object has the following fields for dashboard widgets:

**Agent Status**

| Field Name | Data Type | Notes                                                                     |
| ---------- | --------- | ------------------------------------------------------------------------- |
| summary    | object    | Object with a summary of how many agents are online, offline and disabled |
| agents     | array     | List of agents                                                            |

Each agent in the agent status data response will contain these properties:

| Field Name | Data Type | Notes                                                                                            |
| ---------- | --------- | ------------------------------------------------------------------------------------------------ |
| agentId    | string    | ID of the agent                                                                                  |
| status     | string    | `ONLINE`, `OFFLINE` or `DISABLED`                                                                |
| ipInfo     | object    | Information about the IP of the agent if `Enterprise` or operating system version for `Endpoint` |
| agentName  | string    | Name of the agent                                                                                |
| location   | object    | Contains the latitude, longitude and locationName of the agent                                   |

**Alert List**

| Field Name   | Data Type | Notes                                                                  |
| ------------ | --------- | ---------------------------------------------------------------------- |
| totalAlerts  | integer   | Total number of alerts that were active within the timespan configured |
| activeAlerts | integer   | Number of the alerts that are still active                             |
| alerts       | array     | array of alerts                                                        |

Each alert in the alert list data response will contain these properties:

| Field Name        | Data Type | Notes                                                                                                 |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------- |
| active            | boolean   | `true` or `false`                                                                                     |
| alertId           | integer   | ID of the alert                                                                                       |
| testId            | integer   | ID of the test                                                                                        |
| sourceId          | integer   | ID of the agent, monitor or device producing the alert                                                |
| sourceName        | string    | Name of the agent, monitor or device producing the alert                                              |
| alertRule         | string    | Name of the alert rule that this alert belongs to                                                     |
| alertType         | string    | Name of the alert type                                                                                |
| startTime         | string    | Date when the alert was first active                                                                  |
| durationInSeconds | integer   | Number of seconds the alert was active. If it’s still active, this number will increase every second. |

**Test Table**

This widget accepts the following query params to paginate the response:

* `rows={integer}` optional, the number of alerts in the response. The default value is 10.
* `page={integer}` optional, specifies the page number for the data response. The default value is 1.
* `sortProperty={string}` optional, specifies the property to sort by. The possible values are `alertStatus`, `testName` or `testType`. The ordering may differ from the web application. The default value is `alertStatus`.

| Field Name | Data Type | Notes        |
| ---------- | --------- | ------------ |
| tests      | array     | List of test |

Each test in the test table data response will contain these properties:

| Field Name  | Data Type | Notes                                                           |
| ----------- | --------- | --------------------------------------------------------------- |
| testId      | integer   | ID of the test                                                  |
| testName    | string    | Name of the test                                                |
| target      | string    | Target configured in the test                                   |
| testType    | string    | Type of test                                                    |
| alertStatus | integer   | Number of active alerts for the test                            |
| isShared    | boolean   | Flag set to true if the test has been shared                    |
| graphlets   | array     | List of timeseries points for test metrics in the last 12 hours |

Each graphlet object will contain these properties:

| Field Name | Data Type | Notes                                                                                       |
| ---------- | --------- | ------------------------------------------------------------------------------------------- |
| metric     | string    | Name of the metric                                                                          |
| testId     | integer   | ID of the test                                                                              |
| points     | array     | List of `x` and `y` datapoints where `x` is the timestamp of the point and `y` is the value |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 27 Jul 2022 14:29:51 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 969 X-Organization-Rate-Limit-Reset: 1492093800 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "from": "2022-07-23 00:00:00", "to": "2022-07-24 00:00:00", "reportDataComponentData": { "binSize": 3600, "data": [ { "binId": 1492002000, "count": 10042, "groups": [ { "groupProperty": "Continents", "groupValue": "APNIC" } ], "value": 4236.95 }, { "binId": 1492002000, "count": 16112, "groups": [ { "groupProperty": "Continents", "groupValue": "ARIN" } ], "value": 3801.1 }, ... ], "groupLabelMaps": [] }, }` For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/dashboard-snapshots/{snapshotId}/delete` Deleting a dashboard snapshot](broken-reference)

Deletes the specified dashboard snapshot in ThousandEyes, based on the snapshotId provided in the API request. Users with the `Edit dashboards for all users in account group` permission (Account Admin) can delete any dashboard snapshot.

#### Parameters <a href="#parameters" id="parameters"></a>

* `format=json|xml` Optional. Specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information.
* `aid={aid}` Optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `{snapshotId}` The ID of the dashboard snapshot you would like to delete

#### Response <a href="#response" id="response"></a>

If the dashboard snapshot is successfully deleted, an HTTP 204 NO CONTENT response will be returned. If user lacks the permissions to delete the dashboard snapshot, an HTTP 401 UNAUTHORIZED response will be returned.

Response has no body.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/dashboard-snapshots/2bee381c-cc97-49f4-9ef5-1013c97f4124/delete.json \ -d '' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Server: nginx Date: Wed, 27 Jul 2022 09:43:28 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 970 X-Organization-Rate-Limit-Remaining: 968 X-Organization-Rate-Limit-Reset: 1492076520 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
