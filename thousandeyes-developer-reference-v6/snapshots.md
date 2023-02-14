# Snapshots

[`POST /v6/snapshot` Create a new snapshot](broken-reference)

Creates a new snapshot in ThousandEyes, based on properties provided in the POST data. This endpoint requires the `Create snapshot shares` permission be assigned to the role of the user accessing this endpoint.

Regular users are blocked from using any of the POST-based methods.

Important notes related to snapshot creation using this endpoint:

* There is a creation limit of 10 snapshots per Organization per hour.
* Snapshots created using this endpoint will **expire after 30 days**.
* The time range specified with `from` and `to` must be one of the following: 1, 2, 4, 6, 12, 24, 48 hours.
* Endpoint Agent snapshots **cannot be created using this endpoint**.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* request body containing the following fields:

| Field       | Data Type | Required/Optional | Units               | Notes                                              |
| ----------- | --------- | ----------------- | ------------------- | -------------------------------------------------- |
| displayName | string    | Required          | n/a                 | Title of the snapshot                              |
| from        | dateTime  | Required          | yyyy-MM-dd hh:mm:ss | The date/time when the snapshot will start         |
| isPublic    | integer   | Optional          | n/a                 | 0 for saved event, 1 for share link. Defaults to 0 |
| testId      | integer   | Required          | n/a                 | The ID of the test you wish to create a snapshot   |
| to          | dateTime  | Required          | yyyy-MM-dd hh:mm:ss | The date/time when the snapshot will end           |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/snapshot.json \ -d '{ "testId": 19955, "displayName": "Snapshot created through API", "from": "2018-10-06T00:00:00", "to": "2018-10-06T01:00:00", "isPublic": 1 }' \ -H "Content-Type: application/json" \ -H "Accept: application/json" \ -u {email}:{authToken}`

#### Response <a href="#response" id="response"></a>

If the snapshot is successfully created, an HTTP/201 CREATED response will be returned, and the snapshot details will be returned. See the example below:

**Body**

`{ "link": { "displayName": "Snapshot created through API", "endRoundId": 1538787600, "extraParams": "", "linkId": "wdiac", "roundId": 1538784000, "shareDate": "2018-10-19 03:02:01", "sourceTestId": 19955, "startRoundId": 1538784000, "testId": 58856, "uid": 5784, "viewUrl": "https://wdiac.share.thousandeyes.com/view/tests/" }, "test": [] }`

For error responses, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
