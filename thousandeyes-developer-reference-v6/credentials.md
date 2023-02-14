# Credentials

### Credentials

[`GET /v6/credentials` Credential list](broken-reference)

Returns a list of all credentials configured in ThousandEyes.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information.

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field        | Data Type | Units | Notes                                                                                                  |
| ------------ | --------- | ----- | ------------------------------------------------------------------------------------------------------ |
| credentialId | integer   | n/a   | unique ID of the credential                                                                            |
| name         | string    | n/a   | The name of the credential                                                                             |
| value        | string    | n/a   | The value of the credential that will be encrypted (if the user has permission to read sensitive data) |
| apiLinks     | object    | n/a   | The reference to this credential                                                                       |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/credentials.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Fri, 15 Nov 2019 19:17:46 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: 8xb13 Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 211 X-Organization-Rate-Limit-Reset: 1573845480 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "credentials": [ { "credentialId": 405, "name": "Example Credential 1", "apiLinks": [ { "rel": "self", "href": "https://api.thousandeyes.com/v6/credentials/405" } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/credentials/{credentialId}` Credential details](broken-reference)

Returns details for a credential, including test name, reference & value (value is only visible if the user has `View sensitive data in web transaction` permission). The user should have access to this credential by sharing the same account and must have the `View tests` permission.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information.

#### Request <a href="#request" id="request"></a>

* `{credentialId}` the ID of the credential you wish to retrieve
* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

| Field        | Data Type | Units | Notes                                                                                                  |
| ------------ | --------- | ----- | ------------------------------------------------------------------------------------------------------ |
| credentialId | integer   | n/a   | unique ID of the credential                                                                            |
| name         | string    | n/a   | The name of the credential                                                                             |
| value        | string    | n/a   | The value of the credential that will be encrypted (if the user has permission to read sensitive data) |
| apiLinks     | object    | n/a   | The reference to this credential                                                                       |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/credentials/405.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Date: Fri, 15 Nov 2019 19:36:19 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: f72ql Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 228 X-Organization-Rate-Limit-Reset: 1573846620 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "credentials": [ { "credentialId": 405, "name": "Example Credential 1", "apiLinks": [ { "rel": "self", "href": "https://api.thousandeyes.com/v6/credentials/405" } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/credentials/new` Creating a credential](broken-reference)

Creates a new credential in ThousandEyes, based on properties provided in the POST data. In order to create a new credential, the user attempting the creation must have permission to create tests.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information.

#### Request <a href="#request" id="request"></a>

* Request body should contain both a name and value to be set during creation.

| Field | Data Type | Units | Notes                                                                                                  |
| ----- | --------- | ----- | ------------------------------------------------------------------------------------------------------ |
| name  | string    | n/a   | The name of the credential                                                                             |
| value | string    | n/a   | The value of the credential that will be encrypted (if the user has permission to read sensitive data) |

#### Response <a href="#response" id="response"></a>

If a credential is successfully created, an HTTP/201 CREATED response will be returned, and the credential definition (without its value) will be returned.

| Field        | Data Type | Units | Notes                            |
| ------------ | --------- | ----- | -------------------------------- |
| credentialId | integer   | n/a   | unique ID of the credential      |
| name         | string    | n/a   | The name of the credential       |
| apiLinks     | object    | n/a   | The reference to this credential |

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/credentials/new.json \ -d '{ "name": "new_api_credential", "value": "secret p@ssword" }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 201 CREATED Date: Fri, 15 Nov 2019 19:46:31 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding X-Server-Name: 8xb13 Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 239 X-Organization-Rate-Limit-Reset: 1573846620 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

`{ "credentials": [ { "credentialId": 405, "name": "Example Credential 1", "apiLinks": [ { "rel": "self", "href": "https://api.thousandeyes.com/v6/credentials/405" } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/credentials/{credentialId}/update` Updating a credential](broken-reference)

Updates a credential in ThousandEyes, based on properties provided in the POST data. In order to update a credential, the user attempting the creation must have permission to update tests & should have access to the credential (same account)

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information.

#### Request <a href="#request" id="request"></a>

* `{credentialId}` corresponds to the unique ID of the credential to be updated, obtained through the `/credentials` endpoint
* Request body should contain fields to be set during update.

| Field | Data Type | Units | Notes                                                                                                  |
| ----- | --------- | ----- | ------------------------------------------------------------------------------------------------------ |
| name  | string    | n/a   | The name of the credential                                                                             |
| value | string    | n/a   | The value of the credential that will be encrypted (if the user has permission to read sensitive data) |

#### Response <a href="#response" id="response"></a>

If a credential is successfully edited, an HTTP/200 OK response will be returned, and the credential definition (without its value) will be returned.

| Field        | Data Type | Units | Notes                            |
| ------------ | --------- | ----- | -------------------------------- |
| credentialId | integer   | n/a   | unique ID of the credential      |
| name         | string    | n/a   | The name of the credential       |
| apiLinks     | object    | n/a   | The reference to this credential |

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/credentials/405/update.json \ -d '{ "value":"updated password" }' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Mon, 09 May 2016 16:04:24 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 227 X-Organization-Rate-Limit-Reset: 1492608660 Strict-Transport-Security: max-age=31536000 X-Server-Name: 1-2`

**Body**

`{ "credentials": [ { "credentialId": 405, "name": "Example Credential 1", "apiLinks": [ { "rel": "self", "href": "https://api.thousandeyes.com/v6/credentials/405" } ] } ] }`

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/credentials/{credentialId}/delete` Deleting a credential](broken-reference)

Deletes the specified credential in ThousandEyes, based on the credentialID provided in the API request.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information.

#### Request <a href="#request" id="request"></a>

* The request body must be provided, but should be empty

#### Response <a href="#response" id="response"></a>

If a credential is successfully deleted, an HTTP/204 NO CONTENT response will be returned, and an empty JSON response will be in the body of the response.

#### Example <a href="#example" id="example"></a>

The following example is presented for documentation and reference purposes only.

`$ curl -i https://api.thousandeyes.com/v6/credentials/405/delete.json \ -d '' \ -H "Content-Type: application/json" \ -u {email}:{authToken}`

`HTTP/1.1 204 No Content Date: Fri, 15 Nov 2019 20:24:33 GMT Content-Type: application/json;charset=UTF-8 Connection: keep-alive X-Server-Name: fjxcv Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 236 X-Organization-Rate-Limit-Reset: 1573849500 Strict-Transport-Security: max-age=15724800; includeSubDomains Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff`

**Body**

* The body of a delete response will be empty.

For more information on our HTTP response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
