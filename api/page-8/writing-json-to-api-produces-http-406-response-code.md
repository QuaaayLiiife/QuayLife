# Writing JSON to API Produces HTTP 406 Response Code

To create or update ThousandEyes configurations via the ThousandEyes API, users send data via the HTTP POST method. When sending an HTTP POST command to the ThousandEyes API, if you receive an HTTP response code of "406 (Not Acceptable)" when using JSON-formatted data, please check the following:

*   **Verify that your JSON data is valid JSON**

    Check that you have specified valid JSON using an online JSON verification tool, such as

    [JSONLint](http://jsonlint.com/)

    .
*   **Verify all required fields are sent for your test and action (creation or update) and no fields specific to a different test or action**

    For example, when creating an HTTP Server test, omitting the _url_ field or using the Network test's _server_ and _port_ instead of _url_ will result in the 406 status code. See the

    [Test Metadata section](http://developer.thousandeyes.com/v6/tests/#/test\_metadata)

    of the API Documentation for required fields for each test type.
*   **Ensure that your JSON data uses double quotes rather than single quotes**

    Only double quotes are valid for enclosing string values, per the

    [JSON standard.](http://www.json.org/)

    Single quotes must not be used within the JSON data.

For example, when using the curl command from a Bash shell to send data, use single quotes to enclose the data for the `-d` command line switch, and double quotes within the data. Per the

[API documentation](https://developer.thousandeyes.com/v6/tests/)

, the quoting should use the convention in the following example, which uses the Sandbox API account.

**IMPORTANT:** Per the documentation at

[developer.thousandeyes.com](https://developer.thousandeyes.com/)

: "Please note, test creation/modification/deletion is not allowed on the Sandbox API account, and will not work if attempted. The following example is presented for documentation and reference purposes only."

$curl -i https://api.thousandeyes.com/v6/tests/http-server/817/update.json \\

"agents": \[{"agentId": 117}],

"testName": "Edited test name for API network test addition for www.thousandeyes.com"

\-H "Content-Type: application/json" \\

Alternatively, some shell/operating system combinations may not accept single quotes around the JSON data specified with the `-d` switch. If you must enclose the JSON data in double quotes, you will need to escape the double quotes nested in the data. Nested double quotes may be escaped with a backslash. For example:

$curl -i https://api.thousandeyes.com/v6/tests/http-server/817/update.json \\

\-d "{\\"interval\\": 900, \\

\\"agents\\": \[{\\"agentId\\": 117}],

\\"testName\\": \\"Edited test name for API network test addition for www.thousandeyes.com\\"

\-H "Content-Type: application/json" \\

Note that if backslashes are used for the shell to continue across multiple lines, then you may need to escape your escape character by adding a backslash before the backslashes used to escape the double quotes! In this situation, you may instead wish to take advantage of curl's ability to take the JSON data from a file. See the

[curl man page](http://curl.haxx.se/docs/manpage.html)

for more information.

To see what JSON data is actually sent, you may use the curl command-line switch --trace-ascii \<file>. This will write a copy of the data to a file along with the server response, allowing users to determine whether the data is being properly quoted. Here is the relevant portion of the output from the above command when run with the trace:

\=> Send header, 269 bytes (0x10d)

0000: POST /v6/tests/http-server/817/update.json HTTP/1.1

0032: Authorization: Basic bm9yZXBseUB0aG91c2FuZGV5ZXMuY29tOmczNTFtdzV

0072: 4cWh2a21oMXZxNnpmbTUxYzYyd3l6aWIy

0095: User-Agent: curl/7.30.0

00ae: Host: api.thousandeyes.com

00d7: Content-Type: application/json

\=> Send data, 17 bytes (0x11)

The last line indicates that the JSON data was sent with the correct quotation marks. If the JSON data appeared with no double quotes, then that would likely indicate that escaping the double quotes in the JSON payload on the command line is required.

You may verify that the JSON sent is valid JSON using an online JSON verification tool, such as

[JSONLint](http://jsonlint.com/)

.

Alternatively, you may wish to use an application for sending queries to RESTful APIs. A freeware example of such an application is

[Postman](https://www.getpostman.com/)

.
