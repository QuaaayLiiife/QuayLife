# Administrative endpoints

### Administrative endpoints

[`GET /v6/account-groups` Account group list](broken-reference)

Returns a list of all account groups available to the current user. The aid value returned for an account in this list of account groups can be used in queries elsewhere within the app. See [Account Context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information on changing Account Group context.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.
* There are no request parameters for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/account-groups.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of account groups.

| Field            | Data Type | Notes                                                                                           |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------- |
| accountGroupName | string    | value must be unique across account groups in organization                                      |
| aid              | integer   | system-generated unique ID of the account group                                                 |
| current          | integer   | 1 if the request is being made in the context of this account group, 0 otherwise                |
| default          | integer   | 1 if the account group being queried is your user’s login account group, 0 otherwise            |
| organizationName | string    | (optional) name of the organization; only present if user is a member of multiple organizations |

If successful, returns a list of accounts available to the authenticated user. The “default” flag indicates that this is the “login account group” for the current user, and that any query not including an aid parameter will be executed in that account group context.

The “current” flag indicates that this is the account context you are in at present. For example, calling `https://api.thousandeyes.com/v6/account-groups?aid=354` would change the account context, and show current = 1 for account ID 354, even though the user’s default account ID is 353. Data is shown below using this call as an example.

If your user is assigned to account groups that exist in multiple organizations, the “organizationName” field will be shown for each account group.

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "accountGroups": [ { "accountGroupName": "API Sandbox", "aid": 75, "current": 1, "default": 1 } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/account-groups/{aid}` Account group detail](broken-reference)

Returns detailed information about a specific account group. Requires that the user making the request has the `View all account groups settings` permission.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information

#### Request <a href="#request" id="request"></a>

* `aid={aid}` account group to query for detail.
* There is no request body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/account-groups/315.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns details for the requested account group. Metadata for the request is based on the following detail:

| Field                                | Data Type              | Notes                                                                                                                                                                                                                  |
| ------------------------------------ | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| accountGroupName                     | string                 | the name of the account group                                                                                                                                                                                          |
| aid                                  | integer                | unique ID for the account group                                                                                                                                                                                        |
| organizationName                     | string                 | name of the organization (can only be configured by ThousandEyes Customer Success)                                                                                                                                     |
| current                              | integer                | 1 if the request is being made in the context of this account group, 0 otherwise. If you are receiving a 0 response to this request, try making the call with `aid={aid}` querystring parameter to change the response |
| default                              | integer                | 1 if the account group being queried is your user’s login account group, 0 otherwise                                                                                                                                   |
| users                                | array of user objects  | see individual fields below prefixed by `user`                                                                                                                                                                         |
| users.name                           | string                 | user’s display name                                                                                                                                                                                                    |
| users.email                          | string                 | user’s email address                                                                                                                                                                                                   |
| users.uid                            | integer                | unique ID for the user                                                                                                                                                                                                 |
| users.roles                          | array of role objects  | see individual fields below prefixed by `roles`                                                                                                                                                                        |
| users.roles.roleName                 | string                 | name of the role                                                                                                                                                                                                       |
| users.roles.roleId                   | integer                | unique ID of the role                                                                                                                                                                                                  |
| users.roles.hasManagementPermissions | integer                | 1 if the user has management permissions, 0 otherwise                                                                                                                                                                  |
| users.roles.builtin                  | integer                | 1 if the role is built-in, 0 if the role is user-defined                                                                                                                                                               |
| agents                               | array of agent objects | see individual fields below prefixed by `agents`                                                                                                                                                                       |
| agents.agentId                       | integer                | unique ID for the agent                                                                                                                                                                                                |
| agents.agentName                     | string                 | name of the agent                                                                                                                                                                                                      |
| agents.location                      | string                 | location specification                                                                                                                                                                                                 |
| agents.countryId                     | string                 | 2-digit ISO country code                                                                                                                                                                                               |
| agents.prefix                        | string                 | prefix containing agents public IP address                                                                                                                                                                             |
| agents.utilization                   | integer                | utilization percentage of agent; only available if agentState is `Online`                                                                                                                                              |
| agents.ipAddresses                   | array of strings       | array of private IP addresses                                                                                                                                                                                          |
| agents.publicIpAddresses             | array of strings       | array of public IP addresses                                                                                                                                                                                           |
| agents.enabled                       | integer                | 1 for enabled, 0 for disabled                                                                                                                                                                                          |
| agents.keepBrowserCache              | integer                | 0 for normal operation, 1 for retain cache                                                                                                                                                                             |
| agents.lastSeen                      | dateTime               | date last seen in YYYY-mm-dd HH:MM:SS format                                                                                                                                                                           |
| agents.agentType                     | string                 | enterprise, enterprise cluster                                                                                                                                                                                         |
| agents.network                       | string                 | network (including ASN) of agent’s public IP                                                                                                                                                                           |
| agents.agentState                    | string                 | online or offline                                                                                                                                                                                                      |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "accountGroups": [ { "accountGroupName": "Documentation", "aid": 315, "organizationName": "ThousandEyes Internal", "current": 0, "default": 0, "users": [ { "name": "newest username", "email": "dave+documentation@thousandeyes.com", "uid": 1307, "roles": [ { "roleName": "Account Admin", "roleId": 57, "hasManagementPermissions": 0, "builtin": 1 }, { "roleName": "Organization Admin", "roleId": 60, "hasManagementPermissions": 1, "builtin": 1 } ] }, [...] ], "agents": [ { "agentId": 2486, "agentName": "thousandeyes-stg-va-2546", "location": "San Francisco Bay Area", "countryId": "US", "ipAddress": "192.168.1.78", "publicIpAddress": "99.139.65.220", "prefix": "99.128.0.0/11", "ipAddresses": [ "192.168.1.78" ], "publicIpAddresses": [ "99.139.65.220" ], "enabled": 1, "keepBrowserCache": 0, "lastSeen": "2016-04-26 02:44:08", "agentType": "Enterprise", "network": "AT&T Services, Inc. (AS 7018)", "agentState": "Offline" } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/account-groups/new` Creating an account group](broken-reference)

Creates a new account group. Requires the `Edit all account groups` permission.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information

#### Request <a href="#request" id="request"></a>

* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body should contain the following fields:

| Field            | Data Type              | Required/Optional | Notes                                                                                                                                                                                                |
| ---------------- | ---------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| accountGroupName | string                 | required          | the name of the account group                                                                                                                                                                        |
| agents           | array of agent objects | optional          | To grant access to enterprise agents, specify the agent list. `"agents":[{"agentId": 1234}]`. Note that this is not an additive list - the full list must be specified if changing access to agents. |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/account-groups/new \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '{"accountGroupName": "my testing account group"}' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns details for the requested account group. Note that any user assigned to “All Account Groups” is automatically assigned to the new account group. Metadata for the request is based on the following detail:

| Field                                | Data Type             | Notes                                                                                                                                                                                                                  |
| ------------------------------------ | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| accountGroupName                     | string                | the name of the account group                                                                                                                                                                                          |
| aid                                  | integer               | unique ID for the account group                                                                                                                                                                                        |
| organizationName                     | string                | name of the organization (can only be configured by ThousandEyes Customer Success)                                                                                                                                     |
| current                              | integer               | 1 if the request is being made in the context of this account group, 0 otherwise. If you are receiving a 0 response to this request, try making the call with `aid={aid}` querystring parameter to change the response |
| default                              | integer               | 1 if the account group being queried is your user’s login account group, otherwise 0.                                                                                                                                  |
| users                                | array of user objects | see individual fields below prefixed by `user`                                                                                                                                                                         |
| users.name                           | string                | user’s display name                                                                                                                                                                                                    |
| users.email                          | string                | user’s email address                                                                                                                                                                                                   |
| users.uid                            | integer               | unique ID for the user                                                                                                                                                                                                 |
| users.roles                          | array of role objects | see individual fields below prefixed by `roles`                                                                                                                                                                        |
| users.roles.roleName                 | string                | name of the role                                                                                                                                                                                                       |
| users.roles.roleId                   | integer               | unique ID of the role                                                                                                                                                                                                  |
| users.roles.hasManagementPermissions | integer               | 1 if the user has management permissions, 0 otherwise                                                                                                                                                                  |
| users.roles.builtin                  | integer               | 1 if the role is built-in, 0 if the role is user-defined                                                                                                                                                               |

`HTTP/1.1 201 Created Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "accountGroups": [ { "accountGroupName": "my testing account group", "aid": 9881, "organizationName": "ThousandEyes Internal", "current": 0, "default": 0, "users": [ { "name": "newest username", "email": "dave+documentation@thousandeyes.com", "uid": 1307, "roles": [ { "roleName": "Organization Admin", "roleId": 60, "hasManagementPermissions": 1, "builtin": 1 } ] }, [...] ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/account-groups/{aid}/update` Updating an account group](broken-reference)

Modifies an account group. This can include changing the account group’s name, or modifying the list of users assigned to the account group.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information

#### Request <a href="#request" id="request"></a>

* `aid={aid}` account group to query for detail.
* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body allows update of certain account group fields:

| Field            | Data Type              | Required/Optional | Notes                                                                                                                                                                                                |
| ---------------- | ---------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| accountGroupName | string                 | optional          | name of the account group. To rename the account group, specify a new name.                                                                                                                          |
| agents           | array of agent objects | optional          | To grant access to enterprise agents, specify the agent list. `"agents":[{"agentId": 1234}]`. Note that this is not an additive list - the full list must be specified if changing access to agents. |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/account-groups/315/update \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '{ "accountGroupName": "Renamed account group" }' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns an HTTP/200 status code, as well as the updated account group object.

| Field                                | Data Type             | Notes                                                                                                                                                                                                                  |
| ------------------------------------ | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| accountGroupName                     | string                | the name of the account group                                                                                                                                                                                          |
| aid                                  | integer               | unique ID for the account group                                                                                                                                                                                        |
| organizationName                     | string                | name of the organization (can only be configured by ThousandEyes Customer Success)                                                                                                                                     |
| current                              | integer               | 1 if the request is being made in the context of this account group, 0 otherwise. If you are receiving a 0 response to this request, try making the call with `aid={aid}` querystring parameter to change the response |
| default                              | integer               | 1 if the account group being queried is your user’s login account group, otherwise 0.                                                                                                                                  |
| users                                | array of user objects | see individual fields below prefixed by `user`                                                                                                                                                                         |
| users.name                           | string                | user’s display name                                                                                                                                                                                                    |
| users.email                          | string                | user’s email address                                                                                                                                                                                                   |
| users.uid                            | integer               | unique ID for the user                                                                                                                                                                                                 |
| users.roles                          | array of role objects | see individual fields below prefixed by `roles`                                                                                                                                                                        |
| users.roles.roleName                 | string                | name of the role                                                                                                                                                                                                       |
| users.roles.roleId                   | integer               | unique ID of the role                                                                                                                                                                                                  |
| users.roles.hasManagementPermissions | integer               | 1 if the user has management permissions, 0 otherwise                                                                                                                                                                  |
| users.roles.builtin                  | integer               | 1 if the role is built-in, 0 if the role is user-defined                                                                                                                                                               |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "accountGroups": [ { "accountGroupName": "Renamed accounts group", "aid": 315, "organizationName": "ThousandEyes Internal", "current": 1, "default": 1, "users": [...] "agents": [...] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/account-groups/{aid}/delete` Deleting an account group](broken-reference)

Deletes an account group. Requires the following permissions to be assigned to the user making the request:

* Assign management permissions
* Delete account
* Edit all account groups

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the organization context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error. This must not match the account group to be deleted.

#### Request <a href="#request" id="request"></a>

* `{aid}` account group to delete.
* There is no request body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/account-groups/31415/delete.json \ -d '' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If the deletion is successful, will return an HTTP/204 response code with an empty response body.

`HTTP/1.1 204 No Content Server: nginx Date: Sat, 04 Jul 2020 16:21:59 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 223 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: shplv`

**Body**

Empty response body.

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/users` User list](broken-reference)

Returns the list of all users that belong to the Organization, your selected aid is part of. Returns detailed information about a specific user. Requires that the user making the request has the `API Access` and `View all users` permissions. See [Account Context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information on changing Account Group context.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.
* There are no request parameters for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/users.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns a list of users assigned to the current account group.

| Field                              | Data Type           | Notes                                            |
| ---------------------------------- | ------------------- | ------------------------------------------------ |
| name                               | string              | the name of the user                             |
| email                              | string              | email address for the user                       |
| uid                                | integer             | unique user ID for the user                      |
| lastLogin                          | dateTime            | the last login of the user (UTC)                 |
| dateRegistered                     | dateTime            | the date the user registered their account (UTC) |
| loginAccountGroup                  | accountGroup object | login accountGroup for the user                  |
| loginAccountGroup.accountGroupName | string              | name of the accountGroup                         |
| loginAccountGroup.aid              | integer             | system-generated unique ID of the account group  |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "users": [ { "dateRegistered": "2012-06-27 17:23:50", "email": "noreply@thousandeyes.com", "lastLogin": "2013-11-26 17:53:42", "loginAccountGroup": { "accountGroupName": "API Sandbox", "aid": 75 }, "name": "API Sandbox User", "uid": 245 }, ... ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/users/{uid}` User detail](broken-reference)

Returns detailed information about a specific user. Requires that the user making the request has the `API Access` and `View all users` permissions.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `uid={uid}` unique ID for the user to query for detail.
* There is no body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/users/245.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns details for the requested user. If the user is explicitly assigned to multiple account groups, each account group will explicitly be shown. If the user is assigned to “All Account Groups”, then there will be a special entry for the user using the `allAccountGroupRoles` object.

| Field                                               | Data Type                        | Notes                                                                                            |
| --------------------------------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------ |
| name                                                | string                           | the name of the user                                                                             |
| email                                               | string                           | email address for the user                                                                       |
| uid                                                 | integer                          | unique user ID for the user                                                                      |
| lastLogin                                           | dateTime                         | the last login of the user (UTC)                                                                 |
| dateRegistered                                      | dateTime                         | the date the user registered their account (UTC)                                                 |
| loginAccountGroup                                   | accountGroup object              | login accountGroup for the user                                                                  |
| loginAccountGroup.accountGroupName                  | string                           | name of the accountGroup                                                                         |
| loginAccountGroup.aid                               | integer                          | system-generated unique ID of the account group                                                  |
| accountGroupRoles                                   | list of accountGroupRole objects | see below                                                                                        |
| accountGroupRoles.accountGroup.accountGroupName     | string                           | name of the accountGroup                                                                         |
| accountGroupRoles.accountGroupName.aid              | integer                          | unique account ID for the accountGroup                                                           |
| accountGroupRoles.roles.roleName                    | string                           | the name of the role                                                                             |
| accountGroupRoles.roles.roleID                      | integer                          | system-defined unique ID of the role                                                             |
| accountGroupRoles.roles.hasManagementPermissions    | integer                          | 1 for roles with management permissions, 0 for roles without                                     |
| accountGroupRoles.roles.builtin                     | integer                          | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |
| allAccountGroupRoles                                | list of roles objects            | see below                                                                                        |
| allAccountGroupRoles.roles.roleName                 | string                           | the name of the role                                                                             |
| allAccountGroupRoles.roles.roleID                   | integer                          | system-defined unique ID of the role                                                             |
| allAccountGroupRoles.roles.hasManagementPermissions | integer                          | 1 for roles with management permissions, 0 for roles without                                     |
| allAccountGroupRoles.roles.builtin                  | integer                          | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for                    |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "users": [ { "accountGroupRoles": [ { "accountGroup": { "accountGroupName": "API Sandbox", "aid": 75 }, "roles": [ { "builtin": 0, "hasManagementPermissions": 1, "roleId": 280871, "roleName": "API User" } ] } ], "dateRegistered": "2012-06-27 17:23:50", "email": "noreply@thousandeyes.com", "lastLogin": "2013-11-26 17:53:42", "loginAccountGroup": { "accountGroupName": "API Sandbox", "aid": 75 }, "name": "API Sandbox User", "uid": 245 } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/users/new` Adding a user](broken-reference)

Creates a new user.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body should contain the following fields:

| Field                                  | Data Type                        | Required/Optional                     | Notes                                                                                                                                                                                                                    |
| -------------------------------------- | -------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name                                   | string                           | optional                              | the name of the user                                                                                                                                                                                                     |
| email                                  | string                           | required                              | email address for the user                                                                                                                                                                                               |
| loginAccountGroup                      | accountGroup object              | required                              | login accountGroup for the user. If the user being added is already associated with another ThousandEyes organization, this value will be ignored. The user (once added) can modify his default account group as needed. |
| loginAccountGroup.aid                  | integer                          | required for loginAccountGroup object | system-generated unique ID of the account group                                                                                                                                                                          |
| accountGroupRoles                      | list of accountGroupRole objects | see notes                             | see below; either the accountGroupRoles object or the allAccountGroupRoles object must be specified.                                                                                                                     |
| accountGroupRoles.accountGroupName.aid | integer                          | required for accountGroupName object  | unique account ID for the accountGroupName                                                                                                                                                                               |
| accountGroupRoles.roles.roleID         | integer                          | required for roles object             | system-defined unique ID of the role                                                                                                                                                                                     |
| allAccountGroupRoles                   | list of roles objects            | optional                              | either the accountGroupRoles object or the allAccountGroupRoles object must be specified.                                                                                                                                |
| allAccountGroupRoles.roles.roleID      | integer                          | required for roles object             | system-defined unique ID of the role                                                                                                                                                                                     |

A few notes on the topic of user creation:

* If the user is already a member of another ThousandEyes customer’s organization, the user will need to set their own login account group.
* Any update which contains accountGroupRoles is a replace-based update, rather than a delta-based update.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/users/new \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '{ "name":"newest username", "email":"dave+documentationNEW@thousandeyes.com", "loginAccountGroup": { "aid":691 }, "accountGroupRoles":[ { "accountGroup": { "aid":315 }, "roles":[ { "roleId":57 } ] }, { "accountGroup": { "aid":691 }, "roles":[ { "roleId":60 } ] } ], "allAccountGroupRoles": [ { "roleId": 1140 } ] }' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If the request is successful, returns an object in the same format as the user detail endpoint. In the event that the request fails, check the response body for more information.

| Field                                               | Data Type                        | Notes                                                                                            |
| --------------------------------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------ |
| name                                                | string                           | the name of the user                                                                             |
| email                                               | string                           | email address for the user                                                                       |
| uid                                                 | integer                          | unique user ID for the user                                                                      |
| loginAccountGroup                                   | accountGroup object              | login accountGroup for the user                                                                  |
| loginAccountGroup.accountGroupName                  | string                           | name of the accountGroup                                                                         |
| loginAccountGroup.aid                               | integer                          | system-generated unique ID of the account group                                                  |
| accountGroupRoles                                   | list of accountGroupRole objects | see below                                                                                        |
| accountGroupRoles.accountGroup.accountGroupName     | string                           | name of the accountGroup                                                                         |
| accountGroupRoles.accountGroupName.aid              | integer                          | unique account ID for the accountGroup                                                           |
| accountGroupRoles.roles.roleName                    | string                           | the name of the role                                                                             |
| accountGroupRoles.roles.roleID                      | integer                          | system-defined unique ID of the role                                                             |
| accountGroupRoles.roles.hasManagementPermissions    | integer                          | 1 for roles with management permissions, 0 for roles without                                     |
| accountGroupRoles.roles.builtin                     | integer                          | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |
| allAccountGroupRoles                                | list of roles objects            | see below                                                                                        |
| allAccountGroupRoles.roles.roleName                 | string                           | the name of the role                                                                             |
| allAccountGroupRoles.roles.roleID                   | integer                          | system-defined unique ID of the role                                                             |
| allAccountGroupRoles.roles.hasManagementPermissions | integer                          | 1 for roles with management permissions, 0 for roles without                                     |
| allAccountGroupRoles.roles.builtin                  | integer                          | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for                    |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "users": [ { "name": "My new user", "email": "dave+apitesting@thousandeyes.com", "uid": 3914, "loginAccountGroup": { "accountGroupName": "Documentation", "aid": 315 }, "accountGroupRoles": [ { "accountGroup": { "accountGroupName": "Doc Account 2", "aid": 691 }, "roles": [ { "roleName": "Organization Admin", "roleId": 60, "hasManagementPermissions": 1, "builtin": 1 } ] }, { "accountGroup": { "accountGroupName": "Documentation", "aid": 315 }, "roles": [ { "roleName": "Account Admin", "roleId": 57, "hasManagementPermissions": 0, "builtin": 1 } ] } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/users/{uid}/update` Updating a user](broken-reference)

Modifies a user. This can include changing the user’s name, email address, account group assignments, or roles. Use of this endpoint requires the `Edit users in all account groups` or `Edit users` permission.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `uid={uid}` is the unique user ID for the user
* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body allows update of certain user fields:

| Field                                  | Data Type                        | Required/Optional                     | Notes                                           |
| -------------------------------------- | -------------------------------- | ------------------------------------- | ----------------------------------------------- |
| name                                   | string                           | required                              | the name of the user                            |
| email                                  | string                           | required                              | email address for the user                      |
| loginAccountGroup                      | accountGroup object              | required                              | login accountGroup for the user                 |
| loginAccountGroup.aid                  | integer                          | required for loginAccountGroup object | system-generated unique ID of the account group |
| accountGroupRoles                      | list of accountGroupRole objects | optional                              | see below                                       |
| accountGroupRoles.accountGroupName.aid | integer                          | required for accountGroupName object  | unique account ID for the accountGroup          |
| accountGroupRoles.roles.roleID         | integer                          | required for roles object             | system-defined unique ID of the role            |
| allAccountGroupRoles                   | list of roles objects            | optional                              | see below                                       |
| allAccountGroupRoles.roles.roleID      | integer                          | required for roles object             | system-defined unique ID of the role            |

A few notes on the topic of user modifications:

* If a user’s email is updated, the user will need to validate the username change before being able to subsequently log in, or execute API operations.
* Any update which contains accountGroupRoles is a replace-based update, rather than a delta-based update.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/users/1390/update \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '{ "name":"newest username", "email":"dave+documentationNEW@thousandeyes.com", "loginAccountGroup": { "aid":691 }, "accountGroupRoles":[ { "accountGroup": { "aid":315 }, "roles":[ { "roleId":57 } ] }, { "accountGroup": { "aid":691 }, "roles":[ { "roleId":60 } ] } ], "allAccountGroupRoles": [ { "roleId": 1140 } ] }' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns an updated user object in the same format as the user detail endpoint.

| Field                                               | Data Type                        | Notes                                                                                            |
| --------------------------------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------ |
| name                                                | string                           | the name of the user                                                                             |
| email                                               | string                           | email address for the user                                                                       |
| uid                                                 | integer                          | unique user ID for the user                                                                      |
| loginAccountGroup                                   | accountGroup object              | login accountGroup for the user                                                                  |
| loginAccountGroup.accountGroupName                  | string                           | name of the accountGroup                                                                         |
| loginAccountGroup.aid                               | integer                          | system-generated unique ID of the account group                                                  |
| lastLogin                                           | dateTime                         | the last login of the user (UTC)                                                                 |
| dateRegistered                                      | dateTime                         | the date the user registered their account (UTC)                                                 |
| accountGroupRoles                                   | list of accountGroupRole objects | see below                                                                                        |
| accountGroupRoles.accountGroup.accountGroupName     | string                           | name of the accountGroup                                                                         |
| accountGroupRoles.accountGroupName.aid              | integer                          | unique account ID for the accountGroup                                                           |
| accountGroupRoles.roles.roleName                    | string                           | the name of the role                                                                             |
| accountGroupRoles.roles.roleID                      | integer                          | system-defined unique ID of the role                                                             |
| accountGroupRoles.roles.hasManagementPermissions    | integer                          | 1 for roles with management permissions, 0 for roles without                                     |
| accountGroupRoles.roles.builtin                     | integer                          | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |
| allAccountGroupRoles                                | list of roles objects            | see below                                                                                        |
| allAccountGroupRoles.roles.roleName                 | string                           | the name of the role                                                                             |
| allAccountGroupRoles.roles.roleID                   | integer                          | system-defined unique ID of the role                                                             |
| allAccountGroupRoles.roles.hasManagementPermissions | integer                          | 1 for roles with management permissions, 0 for roles without                                     |
| allAccountGroupRoles.roles.builtin                  | integer                          | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for                    |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "users": [ { "name": "newest username", "email": "dave+documentationNEW@thousandeyes.com", "uid": 1307, "loginAccountGroup": { "accountGroupName": "Doc Account 2", "aid": 691 }, "lastLogin": "2016-10-14 01:27:39", "dateRegistered": "2013-03-29 19:57:23", "accountGroupRoles": [ { "accountGroup": { "accountGroupName": "Doc Account 2", "aid": 691 }, "roles": [ { "roleName": "Organization Admin", "roleId": 60, "hasManagementPermissions": 1, "builtin": 1 } ] }, { "accountGroup": { "accountGroupName": "Documentation", "aid": 315 }, "roles": [ { "roleName": "Account Admin", "roleId": 57, "hasManagementPermissions": 0, "builtin": 1 } ] } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/users/{uid}/delete` Deleting a user](broken-reference)

Deletes a user. Requires `Edit users in all account groups` or `Edit users` permissions to be assigned to the user making the request.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `uid={uid}` is the unique user ID for the user to delete.
* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* There is no request body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl -i https://api.thousandeyes.com/v6/users/3914/delete.json \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If the deletion is successful, will return an HTTP/204 response code with an empty response body.

`HTTP/1.1 204 No Content Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

Empty response body.

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/roles` Role list](broken-reference)

Returns a list of all roles defined and visible to the current user.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.
* There are no request parameters for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/roles.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of roles defined in the system.

| Field                    | Data Type | Notes                                                                                            |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------ |
| roleName                 | string    | the name of the role                                                                             |
| roleId                   | integer   | unique ID of the role                                                                            |
| hasManagementPermissions | integer   | if the role is assigned any management permissions, this value will be 1. Otherwise, 0           |
| builtin                  | integer   | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "roles": [ { "builtin": 1, "hasManagementPermissions": 1, "roleId": 156, "roleName": "Account Admin" }, { "builtin": 0, "hasManagementPermissions": 1, "roleId": 280871, "roleName": "API User" }, { "builtin": 1, "hasManagementPermissions": 1, "roleId": 159, "roleName": "Organization Admin" }, { "builtin": 1, "hasManagementPermissions": 0, "roleId": 162, "roleName": "Regular User" } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/roles/{roleId}` Role detail](broken-reference)

Returns detailed information about a role, defining role name, ID and assigned permissions.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `{roleId}` is the unique ID for the role
* There is no request body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/roles/280871.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns role details, including role name and assigned permissions.

| Field                              | Data Type                  | Notes                                                                                            |
| ---------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| roleName                           | string                     | the name of the role                                                                             |
| roleId                             | integer                    | unique ID of the role                                                                            |
| hasManagementPermissions           | integer                    | if the role is assigned any management permissions, this value will be 1. Otherwise, 0           |
| builtin                            | integer                    | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |
| permissions                        | list of permission objects | see below                                                                                        |
| permissions.permissionId           | integer                    | system-defined unique ID of the permission                                                       |
| permissions.label                  | string                     | label corresponding to the permission                                                            |
| permissions.isManagementPermission | integer                    | 1 if the permission is classified as a management permission, 0 Otherwise                        |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "roles": [ { "builtin": 0, "roleId": 280871, "roleName": "API User", "permissions": [ { "isManagementPermission": 0, "label": "View reports", "permissionId": 8 }, { "isManagementPermission": 0, "label": "View snapshots", "permissionId": 11 }, ... ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/roles/new` Creating a role](broken-reference)

Allows creation of a role, programmatically.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body should contain the following fields:

| Field                    | Data Type                  | Required/Optional               | Notes                                      |
| ------------------------ | -------------------------- | ------------------------------- | ------------------------------------------ |
| roleName                 | string                     | required                        | the name of the role                       |
| permissions              | list of permission objects | optional                        | see below                                  |
| permissions.permissionId | integer                    | required for permissions object | system-defined unique ID of the permission |

A few notes on the topic of role creation:

* Post with a role name, and permissions that need to be assigned to the role.
* Permission definitions and details can be obtained from the [permissions](broken-reference) endpoint.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/roles/new \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '{ "roleName": "My new role", "permissions": [ { "permissionId": 1 }, { "permissionId": 2 } ] }' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns role details, including role name and assigned permissions.

| Field                              | Data Type                  | Notes                                                                                            |
| ---------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| roleName                           | string                     | the name of the role                                                                             |
| roleId                             | integer                    | unique ID of the role                                                                            |
| builtin                            | integer                    | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |
| permissions                        | list of permission objects | see below                                                                                        |
| permissions.permissionId           | integer                    | system-defined unique ID of the permission                                                       |
| permissions.label                  | string                     | label corresponding to the permission                                                            |
| permissions.isManagementPermission | integer                    | 1 if the permission is classified as a management permission, 0 Otherwise                        |

`HTTP/1.1 201 Created Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "roles": [ { "roleName": "My new role", "roleId": 57, "builtin": 0, "permissions": [ { "permissionId": 1, "label": "Assign users emails to alerts", "isManagementPermission": 0 }, [...] ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/roles/{roleId}/update` Updating a role](broken-reference)

Modifies a user-defined role by changing the role name or permissions assigned.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* `{roleId}` is the unique ID for the role
* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body allows update of certain role fields:

| Field                    | Data Type                  | Required/Optional               | Notes                                      |
| ------------------------ | -------------------------- | ------------------------------- | ------------------------------------------ |
| roleName                 | string                     | optional                        | the name of the role                       |
| permissions              | list of permission objects | optional                        | see below (and notes below)                |
| permissions.permissionId | integer                    | required for permissions object | system-defined unique ID of the permission |

A few notes related to role modifications:

* The full list of permissions must be sent, this endpoint does not support a delta-based grant or revocation of permissions.
* Permission definitions and details can be obtained from the [permissions](broken-reference) endpoint.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/roles/57/update \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '{ "roleName": "New name for my role", "permissions": [ { "permissionId": 1 }, { "permissionId": 3 } ] }' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns updated role details, including role name and assigned permissions.

| Field                              | Data Type                  | Notes                                                                                            |
| ---------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| roleName                           | string                     | the name of the role                                                                             |
| roleId                             | integer                    | unique ID of the role                                                                            |
| builtin                            | integer                    | 1 for built-in roles (Account Admin, Organization Admin, Regular User), 0 for user-defined roles |
| permissions                        | list of permission objects | see below                                                                                        |
| permissions.permissionId           | integer                    | system-defined unique ID of the permission                                                       |
| permissions.label                  | string                     | label corresponding to the permission                                                            |
| permissions.isManagementPermission | integer                    | 1 if the permission is classified as a management permission, 0 Otherwise                        |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "roles": [ { "roleName": "New name for my role", "roleId": 57, "builtin": 0, "permissions": [ { "permissionId": 1, "label": "Assign users emails to alerts", "isManagementPermission": 0 }, [...] ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/permissions` Permission list](broken-reference)

Returns a list of all assignable permissions, which is used in the context of modifying roles.

Users must be in a role that is assigned managment permissions in order to access this endpoint. Users without management permissions attempting to access this endpoint will have an HTTP/403 response code returned.

#### Optional Parameters <a href="#optional_parameters" id="optional_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.
* There are no request parameters for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/permissions.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of permissions.

| Field                  | Data Type | Notes                                                                     |
| ---------------------- | --------- | ------------------------------------------------------------------------- |
| permissionId           | integer   | unique ID of the permission                                               |
| label                  | string    | label for the permission (as shown in the ThousandEyes roles interface)   |
| isManagementPermission | integer   | 1 if the permission is classified as a management permission, 0 Otherwise |

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "permissions": [ { "permissionId": 1, "label": "Assign users emails to alerts", "isManagementPermission": 0 }, { "permissionId": 51, "label": "View billing", "isManagementPermission": 1 }, ... ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/audit/user-events/search` Activity log](broken-reference)

Returns a list of activity log events. User with `View activity log for all users in account group` permission can see all activity log events in the current account group. User with `View own activity log` permission can see own activity log events in the current account group. See [Account Context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information on changing Account Group context.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information.
* `window=[0-9]+[smhdw]?` specifies a window of time for the result set. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `from=YYYY-mm-ddTHH:MM:SS&to=YYYY-mm-ddTHH:MM:SS` specifies an explicit start (and optionally, end) for your range of data. See [Time Ranges](https://developer.thousandeyes.com/v6/#/timeranges) for more information.
* `aid={aid}` optional, changes the account group context of the current request. If an invalid account group ID is specified as a parameter, the response will come back as an HTTP/400 error.

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.
* There are no request parameters for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/audit/user-events/search.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back an array of audit events.

| Field            | Data Type | Notes                                           |
| ---------------- | --------- | ----------------------------------------------- |
| accountGroupName | string    | the name of the account group                   |
| aid              | integer   | system-generated unique ID of the account group |
| date             | dateTime  | date of the event in YYYY-mm-dd HH:MM:SS format |
| event            | string    | event type                                      |
| ipAddress        | string    | source IP address of the user                   |
| resources        | array     | array of resources affected by the event        |
| uid              | integer   | unique user ID of the user                      |
| user             | string    | the name and email address of the user          |

Each object in a `resources` array contains the following fields

| Field | Data Type | Notes                                                                                                 |
| ----- | --------- | ----------------------------------------------------------------------------------------------------- |
| name  | string    | name of the affected resource                                                                         |
| type  | string    | type of resource affected. Can be “testName”, “reportTitle”, “userDisplayName”, “alertRuleName”, etc. |

`HTTP/1.1 200 OK Server: nginx Date: Wed, 21 Jun 2017 08:16:10 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 234 X-Organization-Rate-Limit-Reset: 1498033020 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-5`

**Body**

`{ "auditEvents": [ { "accountGroupName": "API Sandbox", "aid": 75, "date": "2017-06-02 18:08:06", "event": "Login failed", "ipAddress": "192.88.158.246", "resources": [], "uid": 245, "user": "API Sandbox User (noreply@thousandeyes.com)" }, { "accountGroupName": "API Sandbox", "aid": 75, "date": "2017-05-02 13:53:31", "event": "Report created", "ipAddress": "192.88.158.246", "resources": [ { "type": "reportTitle", "name": "My New Report" } ], "uid": 245, "user": "API Sandbox User (noreply@thousandeyes.com)" } ], "pages": { "current": 1 } }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/quotas` Obtaining usage quota](broken-reference)

This endpoint returns organization and account groups usage quotas. This endpoint requires the `Edit organization and account group quotas` permission (a management permission). For users who have quota update permission in multiple organizations, the API will return data from all such organizations.

#### Optional Parameters <a href="#optional_parameters" id="optional_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/quotas.json \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

Sends back detailed usage quota information about the organization. Users in roles with insufficient permissions will receive an HTTP/403 response.

| Field              | Data Type                           | Required/Optional | Notes                                                                                                                                    |
| ------------------ | ----------------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| organizationQuota  | object                              | optional          | JSON object with properties `orgId` (optional) and `value`. Null `value` will unset the organization quota                               |
| accountGroupQuotas | list of account group quota objects | optional          | Each account group quota object should have properties `aid` and `value`. Null `value` will unset the account group quota for given aid. |

`HTTP/1.1 200 OK Date: Fri, 17 Jan 2020 17:59:14 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: r1grs Cache-Control: no-store X-Organization-Rate-Limit-Limit: 1000 X-Organization-Rate-Limit-Remaining: 999 X-Organization-Rate-Limit-Reset: 1579284000 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "quotas": [ { "organizationQuota": { "value": 2500000000, "orgId": 1 }, "accountGroupQuotas": [ { "value": 226000, "aid": 100 }, { "value": 268000, "aid": 101 }, { "value": 151000, "aid": 102 } ] }, { "organizationQuota": { "value": 1100000000, "orgId": 2 }, "accountGroupQuotas": [ { "value": 226000, "aid": 200 } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/quotas` Updating usage quotas](broken-reference)

This endpoint allows the user to update organization and account groups usage quotas for all the organizations where user has `Edit organization and account group quotas` permission (a management permission). The successful response will return the latest quota values.

#### Optional (querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information

#### Request <a href="#request" id="request"></a>

* `content-type` and `accept` headers must be set (both to `application/json`) when using this endpoint.
* Request body is an array of JSON objects, that allows the user to update account group and organization quotas for multiple organizations where user has quota update permission. Each JSON object can have these fields below:

| Field              | Data Type                           | Required/Optional | Notes                                                                                                                                    |
| ------------------ | ----------------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| organizationQuota  | object                              | optional          | JSON object with properties `orgId` (optional) and `value`. Null `value` will unset the organization quota                               |
| accountGroupQuotas | list of account group quota objects | optional          | Each account group quota object should have properties `aid` and `value`. Null `value` will unset the account group quota for given aid. |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/quotas/ \ -H "Accept: application/json" \ -H "Content-Type: application/json" \ -d '[ { "organizationQuota": { "value": 2500000000, "orgId": 1 }, "accountGroupQuotas": [ { "value": 226000, "aid": 38036 }, { "value": 268000, "aid": 38730 }, { "value": 151000, "aid": 45022 } ] } ]' \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If successful, returns an HTTP/200 status code, as well as the list of updated usage quotas.

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 233 X-Organization-Rate-Limit-Reset: 1493736900 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-3`

**Body**

`{ "quotas": [ { "organizationQuota": { "value": 2500000000, "orgId": 1 }, "accountGroupQuotas": [ { "value": 226000, "aid": 100 }, { "value": 268000, "aid": 101 }, { "value": 151000, "aid": 102 } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
