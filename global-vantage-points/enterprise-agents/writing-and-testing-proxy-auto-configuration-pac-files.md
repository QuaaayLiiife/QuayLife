# Writing and Testing Proxy Auto-Configuration (PAC) Files

Similar to web browsers, ThousandEyes Enterprise Agents can use a proxy auto-config (PAC) file to select a proxy server based on the requested URL and other variables. A PAC file contains a single JavaScript function named FindProxyForURL, which will return an object containing one or more proxies, or indicate that the client should not use a proxy and instead connect directly to the web server. Each request by a Web Layer test (HTTP Server, Page Load, Transaction and FTP Server) will be parsed by the PAC file to select a proxy or direct access for that request.

This article discusses creation of PAC files for various use cases. Additionally, if the PAC file has many lines or complex logic, the `pactester` utility can be used to check the syntax of PAC file. Information for installation and use of pactester is also presented.

A PAC file is a text file defining a single JavaScript function: FindProxyForURL(url, host). The FindProxyForURL function is run in a restricted JavaScript environment, with only a limited set of standard JavaScript functions available to define FindProxyForURL. A list of supported functions can be found

[here](http://findproxyforurl.com/pac-functions/)

.

ThousandEyes does not recommend the use of the `myIpAddress` function. This condition returns the IP address of the host machine. However, there is no standardized implementation of the function, and this could result in different behavior between the agent and Browserbot.

**FindProxyForUrl arguments**

* **url:** The URL of the request, in the form protocol://hostname:port/path. The hostname can be a domain name or IP address. The port number is optional if the default port is used for the given protocol (e.g port 80 for http URLs or port 443 for https URLs).
*   **host:** The hostname extracted from the URL string.

    Example: For the URL in the example above, the host would be "www.example.com"

The url and host variables are populated by the calling program (in the case of an Enterprise Agent, a process that runs a test, uploads data, performs package upgrades, or other functions) and are available for use within the definition of FindProxyForURL.

**FindProxyForUrl return values**

The return value of the FindProxyForUrl function is the value specified by the JavaScript return function inside the FindProxyForUrl function. The value must be comprised of one or more of the following strings:

| Return value (string)   | Result                                                                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| DIRECT                  | Request in the **url** variable will be sent directly to the web server in the **host** variable (see **FindProxyForUrl arguments** above). |
| PROXY **host**:**port** | Request in the **url** variable will use proxy **host** on port number **port**.                                                            |

Specifying more than one string as a return value provides a fallback mechanism. For example, in the following return statement:

return "PROXY proxy1.example.com; PROXY proxy2.example.com; DIRECT";

if "proxy1.example.com" is unresponsive, the next method specified by the subsequent string will be used, in this case proxying through "proxy2.example.com". If that proxy does not respond, the next request method, "DIRECT" is tried. Multiple strings must be separated by semi-colons. The request method keywords "DIRECT", and "PROXY" are case-sensitive (must be upper-case).

* Proxy fallback is only supported for Page Load and Transaction tests (BrowserBot). HTTP Server and FTP Server tests, as well as administrative connections from the Agent to the ThousandEyes platform do not support any fallback proxy or proxies in the PAC file.
* ThousandEyes tests do not currently support SOCKS-based proxies.

A typical PAC file contains multiple `if` statements, each with a `return` function within the execution block of the if statement. When the conditions of the if statement are met, the block's return statement is executed and the FindProxyForUrl function terminates. No further evaluation is performed. If the conditions of an if statement are not met, processing continues. The last line of a PAC file is typically a return statement without an enclosing if statement, which acts as a "clean-up" or "catch-all" rule. JavaScript comments are permitted using "//" and "/\*" syntax. A basic example of a PAC file:

function FindProxyForURL(url,host)

// Access the internet directly for one site

if (dnsDomainIs(host, "www.example.com")) {

// No proxy for private (RFC 1918) IP addresses (intranet sites)

if (isInNet(dnsResolve(host), "10.0.0.0", "255.0.0.0") ||

isInNet(dnsResolve(host), "172.16.0.0", "255.240.0.0") ||

isInNet(dnsResolve(host), "192.168.0.0", "255.255.0.0")) {

// No proxy for localhost

if (isInNet(dnsResolve(host), "127.0.0.0", "255.0.0.0")) {

// Clean-up rule. Everything else uses a proxy. Note semi-colon delimiter between strings.

return "PROXY proxy1.example.com:8080; PROXY proxy2.example.com:8080; DIRECT";

This example demonstrates the basic PAC file constructs for accessing web sites directly using a return value string of "DIRECT", and for accessing web sites using one or more proxies by returning a string containing the proxy or proxies. The example tests the value of the "host" parameter passed to the function using two functions,

[dnsDomainIs](http://findproxyforurl.com/pac-functions/)

and

[dnsResolve](http://findproxyforurl.com/pac-functions/)

, in "if" statements.

This example also demonstrates a clean-up rule which returns three access methods: two proxies and then the direct access. If the first proxy in the list is not available, the second with be tried after the first request times out. If neither of the two proxies is available, the request will be sent directly to the web server.

#### PAC File Example - JavaScript Variables and Methods <a href="#pac-file-example-javascript-variables-and-methods" id="pac-file-example-javascript-variables-and-methods"></a>

PAC files can declare and use JavaScript variables. Additionally, methods for the allowed JavaScript functions can be used.

function FindProxyForURL(url,host)

// Declare a variable to store the result of DNS resolution

// Avoids multiple lookups (even from cache) and DNS A records with multiple mappings

var host\_ip = dnsResolve(host);

// Declare a variable to store the protocol of the request

// Extract the protocol from the URL using the substring and indexOf methods

var protocol = url.substring(0, url.indexOf(":") - 1);

// No proxy for private (RFC 1918) IP addresses (intranet sites)

// Using host\_ip variable simplifies code for easier reading

if (isInNet(host\_ip, "10.0.0.0", "255.0.0.0") ||

isInNet(host\_ip, "172.16.0.0", "255.240.0.0") ||

isInNet(host\_ip, "192.168.0.0", "255.255.0.0")) {

// No proxy for localhost

if (isInNet(host, "127.0.0.0", "255.0.0.0")) {

//Choose a proxy based on the URL's protocol

if (protocol == "ftp" || protocol == "ftps") {

return "PROXY ftpproxy.example.com:8021";

} else if (protocol == "https") {

return "PROXY sslproxy.example.com:8443";

return "PROXY proxy.example.com:8080";

In this example, we used methods of the allowed JavaScript functions to extract portions of the URL requested, and assigned values to variables which were used to increase the readability and efficiency of the code.

#### PAC File Example - Shell Expressions <a href="#pac-file-example-shell-expressions" id="pac-file-example-shell-expressions"></a>

The shExpMatch function can be used to match the host or url inputs against a

[shell regular expression](https://en.wikibooks.org/wiki/Regular\_Expressions/Shell\_Regular\_Expressions)

. Shell regular expression characters are similar to regular expressions, but have some differences. Be sure to review the syntax of shell expressions if the differences are not familiar.

function FindProxyForURL(url,host)

// For HTTPS URLs, choose a proxy based on the URL's protocol

if (shExpMatch(url, "https://\*")) return "PROXY sslproxy.example.com:8443";

// For HTTP URLs, choose a proxy based on content in the URL's path (file extension)

if (shExpMatch(url, "http://\*/\*.jpg") ||

shExpMatch(url, "http://\*/\*.gif") ||

shExpMatch(url, "http://\*/\*.png")) {

return "PROXY imgproxy.example.com:8080";

return "PROXY proxy.example.com:8080";

In this example, the value of url is compared to shell expressions in two if statements. The first looks for https URLs, and the second for image file extensions, in order to choose the proxy to which the request is sent. Shell expressions can match any part of a URL, such as the URL parameters.

Before installing a PAC file into an Enterprise Agent, the `pactester` utility can be employed to validate the PAC file. The pactester utility uses the

[pacparser](http://pacparser.manugarg.com/)

library, which can be installed on Linux, Mac OS X and Windows. Instructions for installing on Linux operating systems which can support Enterprise Agents are found below. Consult the pacparser documentation for installation on other operating systems.

#### Ubuntu Linux Installation <a href="#ubuntu-linux-installation" id="ubuntu-linux-installation"></a>

Ubuntu Linux provides repositories with the libpacparser1 package, which can be installed with the following steps.

1.  1\.

    Update repository metadata: `sudo apt-get update`
2.  2\.

    Install the libpacparser1 package: `sudo apt-get install libpacparser1`

Installation of libpacparser1 will install the pactester utility in the /usr/bin directory.

#### ThousandEyes Enterprise Agent Docker Container Installation <a href="#thousandeyes-enterprise-agent-docker-container-installation" id="thousandeyes-enterprise-agent-docker-container-installation"></a>

The ThousandEyes Enterprise Agent Docker image is based on Ubuntu Linux. Installation inside a Docker container can be done by invoking a shell in the container from the Docker host, then following the same steps for an Ubuntu Linux installation.

1.  1\.

    On the Docker host, run a bash shell inside the container, using the name of the container as reported by the `docker ps` command: `docker exec -it <container_name> bash`
2.  2\.

    From the bash shell, update repository metadata: `sudo apt-get update`
3.  3\.

    Install the libpacparser1 package: `sudo apt-get install libpacparser1`

**NOTE:** A typical Docker-based Enterprise Agent installation has limited numbers of non-volatile directories, which retain the directories' contents if the container is reinstalled. The contents of the libpacparser1 package will not be installed in a directory that is retained, when the default container installation is used. If the container is reinstalled, the libpacparser1 package will require reinstallation. ThousandEyes recommends installing libpacparser1 on the Docker host rather than inside the Docker container with the Enterprise Agent.

#### Red Hat Enterprise Linux, CentOS and Oracle Linux Installation <a href="#red-hat-enterprise-linux-centos-and-oracle-linux-installation" id="red-hat-enterprise-linux-centos-and-oracle-linux-installation"></a>

Red Hat Enterprise Linux and RHEL-based distributions do not provide a compiled package for pacparser/pactester. Installation requires building the project from source:

1.  1\.

    If needed, install the required build tools: `sudo yum install -y gcc make unzip git` `sudo yum clean all`
2.  2\.

    Clone the project from the git repository: `git clone https://github.com/pacparser/pacparser.git`
3.  3\.

    Build pacparser: `cd pacparser` `make -C src` `make -C src install` `ldconfig`
4.  4\.

    Clean up: `cd ..` `rm -rf pacparser`

Copy your PAC file to the system with `pactester`, and run the following command:

pactester -p pacfile -u URL

Where pacfile is the path to the PAC file to be tested, and URL is the test URL. The output will be the return value chosen for URL. For example, when using the PAC file from the **PAC file example - shell expressions** section, the following command:

pactester -p proxy.pac -u http://thousandeyes.com/images/logo.gif

PROXY imgproxy.example.com:8080

Repeat as needed with different URLs until all return values have been tested.
