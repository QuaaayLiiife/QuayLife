# Network Utilization from Enterprise Agent Test Traffic

Customers who deploy a ThousandEyes Enterprise Agent may wish to know how much network capacity will be utilized by the agent when performing different types of tests. This article presents measurements of several test types to assist network administrators in capacity planning, troubleshooting or other tasks.

Measurements of packets and bytes are presented for the following test types:

* Agent-to-server (TCP + Bandwidth)

The table below presents examples of the number of packets and bytes measured for some test types in a single test round. The measurements are the sum of traffic from the Enterprise Agent and responses from the target.

Test types used the default settings, except where noted in the table. For the DNS server tests, the data represent a test with four targeted DNS servers.

| **Test Type**                     | **Packets** | **Bytes** |
| --------------------------------- | ----------- | --------- |
| Agent-to-server (TCP)             | 245         | 27346     |
| Agent-to-server (TCP + bandwidth) | 806         | 485368    |
| Agent-to-server (ICMP)            | 194         | 28280     |
| DNS server (iterative)            | 16          | 1632      |
| DNS server (recursive)            | 16          | 1632      |
| DNS trace                         | 10          | 1637      |

In the TCP-based agent-to-server tests, the target supports TCP selective acknowledgements (SACK). For a target not supporting TCP SACK the number of packets and bytes are slightly higher:

Detailed information on Network test packet flows can be found

[here](https://docs.thousandeyes.com/product-documentation/advanced-troubleshooting/network-tests-explained)

.

In addition to SACK support, the amount of packets and bytes for a given test type can vary for a number of reasons. Below are some reasons why a test of the same type might not produce identical numbers of packets and bytes.

* The test data above does not reflect included network measurements. For those test types which are configured with included network measurements (**Perform network measurements** checkbox in the **Advanced Settings** tab) add the data from the appropriate TCP-based agent-to-server test to approximate the test's total utilization. For DNS server tests, add this data for each DNS server targeted by the test.
* The number of packets and bytes used can change due to loss in the networks between agent and target. A lossy network path will cause packet retransmission in TCP-based tests, increasing packet and byte counts.
* Test characteristics may change with new releases of software for the ThousandEyes platform.

### Other Network Utilization <a href="#other-network-utilization" id="other-network-utilization"></a>

In addition to network utilization from tests, agents generate additional traffic for administrative purposes such as:

* NTP traffic to synchronize the time on the agent
* DNS resolution for the ThousandEyes collector
* Communication between agent and ThousandEyes collector
* Communication between agent and software repositories to check for and download new software

The first three items in the above list will contribute only small amounts of traffic; the last item may contribute up to some number of megabytes of software download in a short span of time (seconds or minutes) but only infrequently (periods of weeks or months).
