# Endpoint agents

### Endpoint agents

[`GET /v6/endpoint-agents` Listing all agents](broken-reference)

Returns a list of all endpoint agents in a given account group.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information
* `deleted=true|false` specifies if deleted agents should be returned too. By default it is false - only non-deleted agents are returned
* `agentName={agent_name}` returns only agents with a given name
* `computerName={computer_name}` returns only agents with a given computer name

#### Request <a href="#request" id="request"></a>

* There is no request body for this request.

#### Response <a href="#response" id="response"></a>

Sends back an array of endpoint agents. Account groups with a larger number of agents will have the response paginated - details about response pagination can be found [here](https://developer.thousandeyes.com/v6/#/pagination).

Each endpoint agent consists of the following fields:

| Field                    | Data Type | Notes                                                                                                                                       |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId                  | string    | unique ID of the Endpoint agent                                                                                                             |
| agentName                | string    | display name of the agent                                                                                                                   |
| computerName             | string    | display name of the computer                                                                                                                |
| osVersion                | string    | version of the OS computer is running                                                                                                       |
| kernelVersion            | string    | version of the kernel computer is running                                                                                                   |
| manufacturer             | string    | computer hardware manufacturer                                                                                                              |
| model                    | string    | computer hardware model                                                                                                                     |
| totalMemory              | string    | total memory (RAM) of the computer                                                                                                          |
| lastSeen                 | datetime  | last time when agent checked-in                                                                                                             |
| status                   | string    | status of the Endpoint agent in ThousandEyes, set to “enabled” or “disabled”                                                                |
| deleted                  | bool      | set to `true` if the Endpoint agent has been deleted, `false` otherwise                                                                     |
| version                  | string    | version of the Endpoint agent                                                                                                               |
| createdTime              | datetime  | date and time when the Endpoint agent was installed                                                                                         |
| numberOfClients          | integer   | the number of user accounts associated with the machine where the Endpoint agent is installed                                               |
| publicIP                 | string    | public IP of the Endpoint agent used for the most recent check-in                                                                           |
| location                 | object    | location of the Endpoint agent resolved during last check-in, see `location` object below for details                                       |
| clients                  | array     | the user accounts on the machine where the Endpoint agent is installed, see `client` below for details                                      |
| agentType                | string    | type of the Endpoint agent, valid values are “enterprise” for Endpoint agent Enterprise, and “enterprise-pulse” for an Endpoint agent Pulse |
| proxyId                  | integer   | proxyId if the agent is configured to use a proxy server                                                                                    |
| vpnProfiles              | array     | list of VPNs that the Endpoint Agent detected in its last checkin. See `vpnProfile` below for details                                       |
| networkInterfaceProfiles | array     | list of network interfaces. See `interfaceProfile` below for details                                                                        |

Each `client` corresponds to one OS account and consists of the following fields:

| Field             | Data Type | Notes                                                                                                                     |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------- |
| browserExtensions | array     | if installed, details about endpoint browser extensions, see `browserExtensions` object below                             |
| userProfile       | object    | user profile containing a user name. The name is extracted from operating system account when endpoint agent is installed |

`location` object:

| Field        | Data Type | Notes                                            |
| ------------ | --------- | ------------------------------------------------ |
| latitude     | double    | approximate GPS latitude of the Endpoint agent   |
| longitude    | double    | approximate GPS longitude of the Endpoint agent  |
| locationName | string    | geographic name of the Endpoint agent’s location |

`browserExtensions` object:

| Field   | Data Type | Notes                                                                                   |
| ------- | --------- | --------------------------------------------------------------------------------------- |
| browser | string    | name of the browser where the extension is installed, “CHROME,” “EDGE” or “IE”          |
| profile | string    | name of the browser profile where the extension is installed                            |
| version | string    | endpoint agent browser extension version number                                         |
| enabled | bool      | flag indicating if the extension is “disabled” or “enabled” in the web browser          |
| active  | bool      | flag indicating if there is communication between the extension and ThousandEyes portal |
| error   | string    | any errors encountered while getting extension status                                   |

`vpnProfile` object:

| Field                 | Data Type | Notes                                                                                  |
| --------------------- | --------- | -------------------------------------------------------------------------------------- |
| interfaceName         | string    | interface name associated with `interfaceProfile`. See `interfaceProfile` object below |
| vpnType               | string    | name of the VPN provider. For example, “CiscoAnyConnect” or “ZscalerInternet”          |
| vpnGatewayAddress     | string    | IP address of the VPN gateway                                                          |
| vpnClientAddresses    | array     | list of private IP addresses that the VPN server assigned to the device                |
| vpnClientNetworkRange | array     | list of private networks that the VPN server assigned to the device                    |

`interfaceProfile` object:

| Field           | Data Type | Notes                                                                                                                              |
| --------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| interfaceName   | string    | name of the network interface                                                                                                      |
| addressProfiles | array     | an array of address profiles. See `addressProfile` object below                                                                    |
| hardwareType    | enum      | name of hardware type - WIRELESS, ETHERNET, MODEM, VIRTUAL, OTHER or UNKNOWN.                                                      |
| ethernetProfile | object    | this field is present only if the hardware type of this interface is determined to be ETHERNET. See `ethernetProfile` object below |
| wirelessProfile | object    | this field is present only if the hardware type of this interface is determined to be WIRELESS. See `wirelessProfile` object below |

`addressProfile` object:

| Field                 | Data Type | Notes                                                                                                                                                                |
| --------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| addressType           | enum      | the address type. Can be UNIQUE\_LOCAL (an address that is routable only in the scope of a private network) or UNIQUE\_GLOBAL (an address that is globally routable) |
| ipAddress             | string    | IP address of this interface in the network it’s currently connected to                                                                                              |
| prefixLength          | string    | the number of bits representing the network part of ipAddress                                                                                                        |
| gateway               | string    | default gateway for this interface.                                                                                                                                  |
| routerHardwareAddress | string    | router’s MAC address resolved from an ARP request                                                                                                                    |

`ethernetProfile` object:

| Field     | Data Type | Notes              |
| --------- | --------- | ------------------ |
| linkSpeed | integer   | link speed in Mbps |

`wirelessProfile` object:

| Field   | Data Type | Notes                               |
| ------- | --------- | ----------------------------------- |
| bssid   | string    | basic service set identifier (MAC)  |
| ssid    | string    | service set identifier (name)       |
| rssi    | integer   | received signal strength indicator  |
| channel | integer   | wireless network channel            |
| phyMode | string    | physical mode, for example 802.11ac |

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-agents.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "pages": { "next": "https://api.thousandeyes.com/v6/endpoint-agents?pageId=cd9cf945-f66f-4945-b5fe-f7a9a2a97896" }, "endpointAgents": [ { "agentId": "5d0764ac-7e42-4ec8-a0d4-39fc53edccba", "agentName": "test-agent-1", "computerName": "windows machine", "osVersion": "Microsoft Windows 10 Enterprise", "kernelVersion": "10.0.18362", "manufacturer": "LENOVO", "model": "20HR000FUS", "status": "enabled", "deleted": false, "createdTime": "2017-06-29 22:05:36", "lastSeen": "2020-02-20 23:56:43", "version": "0.191.0", "publicIP": "13.227.74.44", "location": { "latitude": 51.51130676269531, "longitude": -0.271392822265625, "locationName": "London, England, UK" }, "clients": [ { "userProfile": { "userName": "pzielinski" }, "browserExtensions": [ { "browser": "CHROME", "profile": "Profile 1", "version": "1.11.0", "installed": true, "enabled": true, "active": true } ] } ], "totalMemory": "16384 MB", "agentType": "enterprise", "vpnProfiles": [ { "vpnGatewayAddress": "18.64.79.52", "vpnType": "CiscoAnyConnect", "vpnClientAddresses": ["10.136.56.58"], "vpnClientNetworkRange": ["10.136.32.0/19"] } ] }, { "agentId": "36ebc26d-19fe-443d-a9bd-cf4ae8f021f0", "agentName": "test-agent-2", "computerName": "mac os", "osVersion": "Version 10.15.2 (Build 19C57)", "kernelVersion": "Darwin 19.2.0", "manufacturer": "Apple, Inc.", "model": "MacBookAir7,2", "status": "enabled", "deleted": false, "createdTime": "2017-06-29 22:05:36", "lastSeen": "2020-02-20 23:56:43", "version": "0.191.0", "publicIP": "13.227.74.43", "location": { "latitude": 51.51130676269531, "longitude": -0.271392822265625, "locationName": "London, England, UK" }, "clients": [ { "userProfile": { "userName": "pzielinski" }, "browserExtensions": [ { "browser": "CHROME", "profile": "Profile 1", "version": "1.11.0", "installed": true, "enabled": true, "active": true } ] } ], "totalMemory": "16384 MB", "agentType": "enterprise", "vpnProfiles": [ { "vpnGatewayAddress": "18.64.79.52", "vpnType": "CiscoAnyConnect", "vpnClientAddresses": ["10.136.56.58"], "vpnClientNetworkRange": ["10.136.32.0/19"] } ], "networkInterfaceProfiles": [ { "interfaceName": "en0", "addressProfiles": [ { "addressType": "UNIQUE_LOCAL", "ipAddress": "192.168.1.64", "prefixLength": 24, "gateway": "192.168.1.254", "routerHardwareAddress": "5c:b1:3e:46:1c:84" } ], "hardwareType": "WIRELESS", "wirelessProfile": { "bssid": "5c:b1:3e:46:1c:87", "ssid": "PLUSNET-2CNJ-5ghz", "rssi": -56, "channel": 48, "phyMode": "802.11ac" } }, { "interfaceName": "utun4", "addressProfiles": [ { "addressType": "UNIQUE_GLOBAL", "ipAddress": "2a01:4b00:bd04:d000:1c63:3302:4092:220d", "prefixLength": 64, "gateway": "fe80::6620:9fff:fe11:58f6", "routerHardwareAddress": "64:20:9f:11:58:f6" }, ], "hardwareType": "VIRTUAL" }] }, }, ... ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`GET /v6/endpoint-agents/{agent_id}` Getting an agent by id](broken-reference)

Returns information about the agent with a given id.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agent_id}` corresponds the unique ID of an endpoint agent, obtained from the `/endpoint-agents` endpoint
* There is no request body for this request

#### Response <a href="#response" id="response"></a>

Returns information about the agent with a given id. See [Listing all agents](http://developer.thousandeyes.com/v6/endpoint\_agents/#/endpoint\_agents\_list) for details of each field.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-agents/5d0764ac-7e42-4ec8-a0d4-39fc53edccba.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAgents": [ { "agentId": "5d0764ac-7e42-4ec8-a0d4-39fc53edccba", "agentName": "test agent 1", "computerName": "Windows machine", "osVersion": "Microsoft Windows 10 Enterprise", "kernelVersion": "10.0.18362", "manufacturer": "LENOVO", "model": "20HR000FUS", "lastSeen": "2020-02-20 23:56:43", "status": "enabled", "deleted": false, "version": "0.191.0", "createdTime": "2017-06-29 22:05:36", "numberOfClients": 3, "publicIP": "13.227.74.44", "location": { "latitude": 51.51130676269531, "longitude": -0.271392822265625, "locationName": "London, England, UK" }, "clients": [ { "userProfile": { "userName": "pzielinski" }, "browserExtensions": [ { "browser": "CHROME", "profile": "Profile 1", "version": "1.11.0", "installed": true, "enabled": true, "active": true } ] } ], "totalMemory": "16384 MB", "agentType": "enterprise", "vpnProfiles": [ { "vpnGatewayAddress": "18.64.79.52", "vpnType": "CiscoAnyConnect", "vpnClientAddresses": [ "10.136.56.58" ], "vpnClientNetworkRange": [ "10.136.32.0/19" ] } ], "networkInterfaceProfiles": [ { "interfaceName": "en0", "addressProfiles": [ { "addressType": "UNIQUE_LOCAL", "ipAddress": "192.168.1.64", "prefixLength": 24, "gateway": "192.168.1.254", "routerHardwareAddress": "5c:b1:3e:46:1c:84" } ], "hardwareType": "WIRELESS", "wirelessProfile": { "bssid": "5c:b1:3e:46:1c:87", "ssid": "PLUSNET-2CNJ-5ghz", "rssi": -56, "channel": 48, "phyMode": "802.11ac" } }, { "interfaceName": "utun4", "addressProfiles": [ { "addressType": "UNIQUE_GLOBAL", "ipAddress": "2a01:4b00:bd04:d000:1c63:3302:4092:220d", "prefixLength": 64, "gateway": "fe80::6620:9fff:fe11:58f6", "routerHardwareAddress": "64:20:9f:11:58:f6" } ], "hardwareType": "VIRTUAL" } ] } ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/endpoint-agents/{agent_id}` Updating an agent](broken-reference)

Updates a given agent with a new name.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agent_id}` corresponds the unique ID of an endpoint agent, obtained from the `/endpoint-agents` endpoint
* Currently the only request body supported is to change the Agent Name, as follows:

`{ "newAgentName":"new name" }`

#### Response <a href="#response" id="response"></a>

Returns information about the updated agent. See [Listing all agents](http://developer.thousandeyes.com/v6/endpoint\_agents/#/endpoint\_agents\_list) for details of each field.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-agents/5d0764ac-7e42-4ec8-a0d4-39fc53edccba.json \ -d '{"newAgentName":"new name"}' \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Fri, 24 Apr 2020 15:59:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1587744000 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAgents": [ { "agentId": "5d0764ac-7e42-4ec8-a0d4-39fc53edccba", "agentName": "new name", "computerName": "Windows machine", "osVersion": "Microsoft Windows 10 Enterprise", "kernelVersion": "10.0.18362", "manufacturer": "LENOVO", "model": "20HR000FUS", "lastSeen": "2020-02-20 23:56:43", "status": "enabled", "deleted": false, "version": "0.191.0", "createdTime": "2017-06-29 22:05:36", "numberOfClients": 3, "publicIP": "13.227.74.44", "location": { "latitude": 51.51130676269531, "longitude": -0.271392822265625, "locationName": "London, England, UK" }, "clients": [ { "userProfile": { "userName": "pzielinski" }, "browserExtensions": [ { "browser": "CHROME", "profile": "Profile 1", "version": "1.11.0", "installed": true, "enabled": true, "active": true } ] } ], "totalMemory": "16384 MB", "agentType": "enterprise" } ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/endpoint-agents/{agent_id}/enable` Enabling an agent](broken-reference)

Enables an agent with a given id.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agent_id}` corresponds the unique ID of an endpoint agent, obtained from the `/endpoint-agents` endpoint
* There is no request body for this request

#### Response <a href="#response" id="response"></a>

Sends back the enabled agent details. See [Listing all agents](http://developer.thousandeyes.com/v6/endpoint\_agents/#/endpoint\_agents\_list) for details of each field.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-agents/5d0764ac-7e42-4ec8-a0d4-39fc53edccba/enable.json \ -d '' \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAgents": [ { "agentId": "5d0764ac-7e42-4ec8-a0d4-39fc53edccba", "agentName": "test-agent-1", "computerName": "Windows machine", "osVersion": "Microsoft Windows 10 Enterprise", "kernelVersion": "10.0.18362", "manufacturer": "LENOVO", "model": "20HR000FUS", "lastSeen": "2020-02-20 23:56:43", "status": "enabled", "deleted": false, "version": "0.191.0", "createdTime": "2017-06-29 22:05:36", "numberOfClients": 3 } ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/endpoint-agents/{agent_id}/disable` Disabling an agent](broken-reference)

Disables an agent with a given id.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agent_id}` corresponds the unique ID of an endpoint agent, obtained from the `/endpoint-agents` endpoint
* There is no request body for this request

#### Response <a href="#response" id="response"></a>

Sends back the disabled agent details. See [Listing all agents](http://developer.thousandeyes.com/v6/endpoint\_agents/#/endpoint\_agents\_list) for details of each field.

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-agents/5d0764ac-7e42-4ec8-a0d4-39fc53edccba/disable.json \ -d '' \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAgents": [ { "agentId": "5d0764ac-7e42-4ec8-a0d4-39fc53edccba", "agentName": "test-agent-1", "computerName": "Windows machine", "osVersion": "Microsoft Windows 10 Enterprise", "kernelVersion": "10.0.18362", "manufacturer": "LENOVO", "model": "20HR000FUS", "lastSeen": "2020-02-20 23:56:43", "status": "disabled", "deleted": false, "version": "0.191.0", "createdTime": "2017-06-29 22:05:36", "numberOfClients": 3 } ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`POST /v6/endpoint-agents/transfer` Transferring an agent](broken-reference)

Triggers a process of transferring a list of agents.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information

#### Request <a href="#request" id="request"></a>

The request’s body should contain a list of agents in CSV format with the following columns (comma delimited):

* “machine\_id” - agent id to be transferred
* “from\_aid” - account id where the agent needs to be transferred from
* “to\_aid” - account id where the agent needs to be transferred to

Example: `machine_id,from_aid,to_aid 5d0764ac-7e42-4ec8-a0d4-39fc53edccba,111,222 5d0764ac-7e42-4ec8-a0d4-39fc53edccba,333,222`

Sending the above body will transfer two agents (“5d0764ac-7e42-4ec8-a0d4-39fc53edccba”, “5d0764ac-7e42-4ec8-a0d4-39fc53edccba”) from accounts 111 and 333 into 222. The calling user needs to have ‘write’ permissions to all accounts submitted in the CSV.

The requests’ media type should be ‘text/csv’ or ‘text/plain’:

`Content-Type: text/plain`

#### Response <a href="#response" id="response"></a>

Returns an object confirming the number of agents to be transferred. Example:

`{ "endpointAgentsTransfer": { "machineCount": 2 } }`

#### Example <a href="#example" id="example"></a>

`$ curl https://api.thousandeyes.com/v6/endpoint-agents/transfer.json \ -d $'machine_id,from_aid,to_aid\n5d0764ac-7e42-4ec8-a0d4-39fc53edccba,111,222\n5d0764ac-7e42-4ec8-a0d4-39fc53edccba,333,222' \ -u {email}:{authToken} \ -H 'content-type: text/csv'`

`HTTP/1.1 200 OK Server: nginx Date: Fri, 18 Mar 2021 15:59:50 GMT Content-Type: text/plain;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237EndpointAgentTransferServiceTest X-Organization-Rate-Limit-Reset: 1587744000 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAgentsTransfer": { "machineCount": 2 } }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).

[`DELETE /v6/endpoint-agents/{agent_id}` Deleting an agent](broken-reference)

Deletes an agent with a given id.

#### Optional (Querystring) Parameters <a href="#optional_querystring_parameters" id="optional_querystring_parameters"></a>

* `format=json|xml` optional, specifies the format of output requested. See [Output Formats](https://developer.thousandeyes.com/v6/#/responseformats) for more information
* `aid={aid}` optional and requires the user to be assigned to the target account group, specifies the account group context of the request, obtained from the `/account-groups` endpoint. Specifying this parameter without the user being assigned to the target account will result in an error response. See [Account group context](https://developer.thousandeyes.com/v6/#/accountcontext) for more information

#### Request <a href="#request" id="request"></a>

* `{agent_id}` corresponds the unique ID of an endpoint agent, obtained from the `/endpoint-agents` endpoint
* There is no request body for this request

#### Response <a href="#response" id="response"></a>

Returns the deleted agent details. See [Listing all agents](http://developer.thousandeyes.com/v6/endpoint\_agents/#/endpoint\_agents\_list) for details of each field.

#### Example <a href="#example" id="example"></a>

`$ curl -X DELETE https://api.thousandeyes.com/v6/endpoint-agents/5d0764ac-7e42-4ec8-a0d4-39fc53edccba.json \ -u {email}:{authToken}`

`HTTP/1.1 200 OK Server: nginx Date: Sat, 25 Aug 2018 17:03:50 GMT Content-Type: application/json;charset=UTF-8 Transfer-Encoding: chunked Connection: keep-alive Cache-Control: no-store X-Organization-Rate-Limit-Limit: 240 X-Organization-Rate-Limit-Remaining: 237 X-Organization-Rate-Limit-Reset: 1535216640 Strict-Transport-Security: max-age=31536000 X-Content-Type-Options: nosniff X-Server-Name: 1-3`

**Body**

`{ "endpointAgents": [ { "agentId": "5d0764ac-7e42-4ec8-a0d4-39fc53edccba", "agentName": "test-agent-1", "computerName": "Windows machine", "osVersion": "Microsoft Windows 10 Enterprise", "kernelVersion": "10.0.18362", "manufacturer": "LENOVO", "model": "20HR000FUS", "lastSeen": "2020-02-20 23:56:43", "status": "disabled", "deleted": true, "version": "0.191.0", "createdTime": "2017-06-29 22:05:36", "numberOfClients": 3 } ] }`

For more information on our response status codes, see the [response status codes documentation](https://developer.thousandeyes.com/v6/#/statuscodes).
