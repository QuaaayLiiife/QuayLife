# Network Overview Shows Packet Loss That Does Not Appear in Path Visualization

On occasion, network layer testing may show packet loss in the

[Network > Overview](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/using-the-network-overview)

view, yet further examination in the

[Network > Path Visualization](broken-reference)

view does not pinpoint the forwarding loss in the network path. The reason for this situation often lies in the difference of the data collection approaches that are used to collect the data for the aforementioned views. If you want to know why, are you ready to go down the rabbit hole?

### How End-to-End Network Measurement Is Performed <a href="#how-end-to-end-network-measurement-is-performed" id="how-end-to-end-network-measurement-is-performed"></a>

When performing end-to-end network tests, the agent sends up to 50 packets to the target. Then, depending on the test type, either target agent counts the received packets and measures the packet arrival timings (

[agent-to-agent](https://docs.thousandeyes.com/product-documentation/tests/agent-to-agent-test-overview)

test type) or the agent that sent the probes counts the received acknowledgment responses (

[agent-to-server](https://docs.thousandeyes.com/product-documentation/advanced-troubleshooting/network-tests-explained)

test type and similar) and uses the count and timing data to calculate loss, latency and jitter values. This constitutes the basis of the end-to-end network measurement.

If end-to-end measurement detects packet loss, the following figure demonstrates how said loss is presented to the user:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a155a6b396513bcfd3f985853a21db62ae2d07fc%2Fproduct-documentation\_tests\_network-overview-shows-packet-loss-that-does-not-appear-in-path-visualization-1.png?alt=media)

In the **Network > Overview** view (1), the loss is presented on the timeline (2), noted in the details (3) and the agents that detected the loss are colored differently in the map view - the more loss is detected, the closer to the red the affected agents' colors are (4).

### How the Network Path Is Discovered <a href="#how-the-network-path-is-discovered" id="how-the-network-path-is-discovered"></a>

The data collection for

[Path Visualization](broken-reference)

, however, operates very differently. When performing path discovery, the testing agent sends sets of probe packets with a sequentially increasing Time to Live (TTL) value in the IP header. Each “node” (routing device) between the testing agent and the test target decrements the TTL by one. When a node receives packets with TTL set to 1 and decrements it to zero, the packet is discarded and the node responds to the packet sender with an ICMP type 11 (Time to Live Exceeded in Transit) message. Once the TTL has been increased high enough for the probe packet to reach the target, the target generates a response that makes the sending agent realize it has reached the end of the network path - the response is either a TCP SYN,ACK or a RST packet, ICMP type 0 (Echo Reply) message or a special UDP response for agent-to-agent tests. Then all path discovery-related information is collected and the data is presented to the user in the **Path Visualization** view:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a18c7559eb789297069c874c4b082ecf6d4391f3%2Fproduct-documentation\_tests\_network-overview-shows-packet-loss-that-does-not-appear-in-path-visualization-2.png?alt=media)

As outlined above, paths from each agent (nodes on the left-hand side) towards the target (the single node on the right-hand side) are rendered and merged where appropriate. Forwarding loss, if it would be detected by the path discovery process, would be indicated with a red ring around the relevant node in the Path Visualization graph.

### Reasons for Loss Result Variation <a href="#reasons-for-loss-result-variation" id="reasons-for-loss-result-variation"></a>

The following conditions are the most common reasons for not being able to pinpoint the event further in the Path Visualization when Network Overview reports the end-to-end packet loss.

Although both, network end-to-end measurement and path discovery processes occur within a specified interval, they may not start at exactly the same moment. If loss events are sporadic or clear rapidly, they may resolve before path discovery is performed.

Additionally, tests are not guaranteed to be run at exactly the same moment from all agents assigned to the test.

Path discovery only sends three packets per TTL value while end-to-end measurement sends a stream of 50 packets directly to the target. Therefore, an individual lost packet has a greater statistical percentage in Path Visualization (33% of packets sent) compared to the end-to-end loss, where a single packet represents only 2% of packets sent. This variation in statistical probability causes differences in the reported loss between the two views.

#### Packet Loss on the Target <a href="#packet-loss-on-the-target" id="packet-loss-on-the-target"></a>

There might be actual packet loss on the target while the path is clean. The traffic drop on the target might be caused by one of the following conditions:

* The SYN backlog on the target is full. The target can't accept new TCP connections and is ignoring all new SYN packets. This only applies to SYN-based TCP measurements.
* The target has reached the ICMP rate limit threshold and is therefore not generating new ICMP responses. This only applies to ICMP-based measurements.
* The target has implemented a rate limiting algorithm and is currently dropping incoming traffic. This condition usually manifests itself as an initial test round showing zero packet loss, followed by one or more test rounds with high packet loss. This alteration between no loss and high loss is often periodic, producing a clearly visible pattern.
* The recipient has an old TCP/IP stack with a "buggy" selective acknowledgment (SACK) implementation. This condition usually manifests itself as a constant low amount of packet loss in SACK-based TCP measurements.
* The target's computing resources have been exhausted. The server can't cope with the network traffic. Although not very likely, this option should not be discarded.

The forwarding loss might not be visible to all agents performing the test, i.e. when the loss is occurring in a network segment that is only traversed by traffic from a single agent. If packets from a single agent are traversing the lossy network segment and one of the Path Visualization probe packets does not get responded with the corresponding ICMP TTL exceeded message, then Path Visualization will not render the affected node with a forwarding loss (red circle). Instead, it will show the missing response as a parallel path with a blank node representing the missing response.

Once the network segment is traversed by traffic from multiple agents, then the missing Path Visualization probe responses are marked as nodes that exhibit forwarding loss, regardless if such loss is detected by one or multiple agents.

### Tips for Further Isolating Network Path Issues <a href="#tips-for-further-isolating-network-path-issues" id="tips-for-further-isolating-network-path-issues"></a>

Here are a few suggestions on how to adjust your testing strategy to pinpoint the network issue that is hard to spot in the Path Visualization.

#### Inspect Multiple Test Rounds of Path Visualization Data <a href="#inspect-multiple-test-rounds-of-path-visualization-data" id="inspect-multiple-test-rounds-of-path-visualization-data"></a>

If a small percentage of loss is consistently observed by the end-to-end measurement for a significant length of time, eventually even the path discovery process will hit the statistical "sweet spot" and show the forwarding loss. To see it, one may need to check multiple rounds of Path Visualization results to spot it.

#### Add More Agents to the Test <a href="#add-more-agents-to-the-test" id="add-more-agents-to-the-test"></a>

Adding more agents to an individual test decreases the statistical influence of false positives or transient events caused by problems local to any individual agent. More agents in different locations will give a more real-world perspective on traffic conditions by using various providers and paths to reach the target.

Adding more agents is especially helpful when the packet loss is occurring closer to the target. Paths from source to target are often wildly different at the start, but then they converge more and more the closer they get to the test target. This makes more and more packets' TTL counters to expire on nodes closer to the target, resulting in a more sensitive forwarding loss detection.

#### Run More Parallel Path Traces <a href="#run-more-parallel-path-traces" id="run-more-parallel-path-traces"></a>

In the test configuration view, in the **Advanced Configuration** tab, there is a setting called **No. of Path Traces**. It governs the number of parallel path discoveries that each agent will perform for this test. Its value defaults to 3 and it can be increased up to 10. Increasing it up to 10 will cause each agent to perform 10 parallel path discoveries in each test round, increasing the probability of successful forwarding loss detection. In this case, the loss sensitivity of each agent is increased and instead of the default 33% forwarding loss detection ability, even a 10% loss will be detected and pinpointed by a single agent.

#### Isolate Return Path Issues <a href="#isolate-return-path-issues" id="isolate-return-path-issues"></a>

Packets often take a different return path on their way back from the test target to the agent. This can make pinpointing the exact location of forwarding loss more difficult in agent-to-server testing because it relies on response packets for accurate measurements. In such cases, an agent-to-agent test can help narrow down the results further. While agent-to-server tests require one agent to record all data, agent-to-agent testing has an agent on each side of the connection, enabling tests to measure unidirectional traffic. For more on configuring agent-to-agent tests, see

[Agent-to-Agent Test Overview](https://docs.thousandeyes.com/product-documentation/tests/agent-to-agent-test-overview)

.

If you are unable to deploy an Enterprise Agent in the same location as the test target (to act as a target for an agent-to-agent test), creating a new test specific to this diagnostic process may help narrow down the scope. To do so, perform the following:

* In your original test's Path Visualization view, identify the furthest node that is functioning normally on the Path Visualization and will respond to pings.
* Configure a new agent-to-server test targeting the node identified above. Use the ICMP protocol.
* Once the initial test results are in, manually verify that the path displayed in the Path Visualization is identical to the original test.

If the results of this new test are free of packet loss and if the discovered path from the new test matches the one observed in the original test, this confirms that the forward path is working as expected, at least up to the node tested in the second test. The loss observed in the original test is, therefore, occurring either on the path between this furthest node tested in the second test and the target or on the reverse path from the target back to the agent.

The following resources provide further information:
