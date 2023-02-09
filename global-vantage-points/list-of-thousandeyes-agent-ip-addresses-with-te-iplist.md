# list of ThousandEyes Agent IP Addresses with te-iplist

You may need the IP addresses of ThousandEyes agents in order to construct firewall rules or similar filters. ThousandEyes does not publish a list of IP addresses, but customers can use the

[ThousandEyes application program interface (API)](https://docs.thousandeyes.com/product-documentation/api/obtaining-a-list-of-thousandeyes-agent-ip-addresses)

to obtain the IP addresses of both Cloud Agents assigned to your organization and Enterprise Agents assigned to your account group. You can query the API with a web browser, a custom script, or a RESTful API tool to obtain the latest list of IP addresses, or you can use our command-line tool: **te-iplist**.

While the list of all ThousandEyes IP addresses can be found via our API, there is no guarantee that a single consistent IP address will be assigned to any ThousandEyes agent. This is because most virtual agents have multiple underlying agents that use different IPs, and tests can be moved between those agents for a number of performance reasons.

When a virtual agent is going to switch to a completely new set of IPs (such as during a provider migration), customers are informed one week in advance via a maintenance announcement on

[ThousandEyes Status](https://status.thousandeyes.com/)

.

To avoid being affected if the IP addresses change, you can filter traffic based on the `user agent string` in the request headers instead.

**te-iplist** is a command-line interface (CLI) utility that queries the ThousandEyes API for the agents available for your account and outputs agents' IPs in different forms (IP list, subnet list, IP range list, IP block list) and formats (plain text, CSV, JSON, XML).

On Linux and macOS, ensure that the utility is executable before you use it:

On macOS Catalina, disable the developer verification warning for this utility:

xattr -d com.apple.quarantine te-iplist

In the **te-iplist** commands illustrated in the sections below, the authentication fields need to be filled in this way:

`<user>` **-** the user's email address `<user-api-token>` **-** the basic authentication token for the API

Display a list of all Cloud and Enterprise Agent IP addresses (`-o ip`):

$ ./te-iplist -u \<user> -t \<user-api-token> -o ip

2400:8900::f03c:91ff:fec8:c7b2

2400:8900::f03c:91ff:fec8:c7d3

2400:8900::f03c:91ff:fedf:65c4

2600:3c03::f03c:91ff:feae:cd41

Display a minimal list of subnets (`-o subnet-loose`) that cover Enterprise Agent IP addresses (`-e`). The list should include agent names as comments (`-n`):

$ ./te-iplist -u \<user> -t \<user-api-token> -o subnet-loose -e -n

10.0.0.3 # kubernetes te-agent-pod

10.0.1.0/26 # ip-10-0-1-48.localdomain; csc-internal; office-12

1.2.3.4 # kubernetes te-agent-pod; ip-10-0-1-48.localdomain; csc-internal; office-12

Display a list of IP blocks (`-o block-strict`) of Cloud Agents' (`-c`) IPv6 (`-6`) addresses:

$ ./te-iplist -u \<user> -t \<user-api-token> -o block-strict -c -6

2400:8900::f03c:91ff:fec8:c7b2

2400:8900::f03c:91ff:fedf:65c4

2403:7000:8000:400::\[18-20]

Display a list of IP ranges (`-o range-strict`) of Enterprise Agents' private (`-e-private`) IPv4 (`-4`) addresses:

$ ./te-iplist -u \<user> -t \<user-api-token> -o range-strict -e-private -4 -n

10.10.10.202 - 10.10.10.203 # primoz-centos-te; centos6

192.168.0.2 - 192.168.0.4 # thousandeyes-va-14244; thousandeyes-va-14403; thousandeyes-va66

Create a comma-separated values (CSV) file that includes all agents and all output formats:

$ ./te-iplist -u \<user> -t \<user-api-token> -o csv > all-agents.csv

You can open the CSV file as a spreadsheet in your favorite spreadsheet editor, such as LibreOffice Calc, Numbers, or Google Sheets. Unfortunately, Microsoft Excel does not support CSV files with newlines inside cells, and will not import the generated CSV.

IP subnets, IP ranges and IP blocks can be displayed in _loose_ or _strict_ notation. Strict notation covers only the IP addresses that are used by the agents. Loose notation covers all IP addresses that are used by the agents, but may also cover some of the addresses that are not used by the agents. Loose notation typically covers all the agent IP addresses with fewer entries. For example, IP addresses:

can be covered by multiple _strict_ subnet notations:

or by a single _loose_ subnet notation:

You should select the notation that is acceptable by your security standards.

Users assigned to multiple account groups can list the agents available in a specific account group with the `-a <accountGroupId>` argument. You can list available account group IDs with the following:

te-iplist -u \<user> -t \<user-api-token> -account-groups

If you don't specify `-a`, **te-iplist** uses the user's login account group. For users in multiple organizations, **te-iplist** assumes only one login account group; to specify multiple account groups, use the `-a` argument to list them.
