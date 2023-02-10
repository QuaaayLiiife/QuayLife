# Single Hop to the Destination

In an included Network test (i.e. part of a DNS or Web Layer test) the ThousandEyes platform uses TCP as the protocol for path tracing rather than ICMP. Because the TCP connection gets terminated on the proxy, hops beyond the proxy cannot be seen. In this scenario, the path visualization will appear something like the image that is shown below. Enterprise Agent 4 is located in a network that does not use an internal proxy, whereas Enterprise Agents 1-3 are in separate data centers, each using a proxy, which is the second hop from the Agents.
