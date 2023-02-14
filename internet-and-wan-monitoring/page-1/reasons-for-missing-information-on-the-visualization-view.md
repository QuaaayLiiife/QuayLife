# Reasons for Missing Information on the Visualization View

For each device your organization controls or can inquire about, determine the answers to the following questions:

**Does the device perform packet filtering?**

Firewalls, routers, load balancers and other network devices can perform packet filtering. Also, the host operating system for a Linux package Enterprise Agent may have a packet filter such as **iptables**, or the target host may employ a packet filter which blocks the outbound ICMP or TCP packets from the Agent, or blocks the inbound ICMP Time-to-Live Exceeded packets returning to the Agent.

It is important to keep in mind that a rule permitting the outbound test packets from the Agent may not be sufficient, even in a stateful firewall or stateful packet filter. A second rule or setting permitting the inbound ICMP Time-to-Live packets may be required if the software does not associate and permit the inbound ICMP Time-to-Live packets.

The effect of packet filtering on the Path Visualization graph depends on which packets are filtered:

* Filtering the outbound TCP or ICMP packets will prevent nodes between the filter (possibly including the filtering device) and the target from appearing on the Path Visualization graph. This will typically include the target node.
*   Filtering the returned/inbound ICMP Time-to-Live Exceeded packets returning to the agent will render nodes between the filter (possibly including the filtering device) and the target as blank nodes on the Path Visualization graph. This will typically not include the target node.

    To address packet filter issues, check your device's packet filtering rules and properties or other global configuration settings, consult your security administrator or the documentation for the device, or contact technical support for the device's manufacturer.

**Does the device perform network address translation (NAT)?**

In addition to packet filtering, network devices such as firewalls, routers, and load balancers can perform network address translation. Translation rules must be in place for NAT'ing the outbound ICMP or TCP packets from the agent and for NAT'ing the inbound ICMP Time-to-Live Exceeded packets returning to the Agent.

Address translation can be done in several ways. For example, most implementations of port-based address translation (PAT, also called one-to-many NAT) typically will not translate the inbound ICMP Time-to-Live Exceeded packets returning to the agent because ICMP packets lack port numbers in their headers. In contrast, a static one-to-one NAT should allow the needed ICMP Time-to-Live Exceeded packets returning to the agent to be correctly translated.

The effect of missing address translation rules on the Path Visualization graph are similar to the effect of packet filtering.

To address address translation issues, check your device's translate rules, consult your security administrator or the documentation for the device, or contact technical support for the device's manufacturer.

**Can the device issue ICMP Time-to-Live Exceeded packets?**

Some devices are configured not to issue ICMP packets or a subset of ICMP packets. For example, a firewall may be configured not to send ICMP packets from itself in order to avoid network scanning or device fingerprinting techniques.

If a packet is received by a device which does not issue ICMP Time-to-Live Exceeded packets, the TTL may still be decremented. But after decrementing, if the TTL = 0 then the packet will be discarded without generating an ICMP Time-to-Live Exceeded packet. The effect is to render the non-TTL generating device as a white node (unknown) on the Path Visualization. See the

[Path Visualization Legend](broken-reference)

for an example.

To permit a device to issue Time-to-Live packets, consult your security administrator or the documentation for the device, or contact technical support for the device's manufacturer.

If your organization's security concerns require that a device not provide information (not issue Time-to-Live Exceeded packets) to unapproved destinations, a packet filter rule can typically be used to drop the packets before they leave the device if the destination is not the ThousandEyes agent.

**Does the device decrement the Time-to-Live field in the IP header?**

If the device does not decrement the value in the TTL field by 1 before routing the packet, then the device cannot issue an ICMP Time-to-Live Exceeded packet (ICMP type 11) because the condition for issuing ICMP type 11 packets is that TTL = 0. A firewall may be configured not to issue ICMP packets in order to avoid network scanning or device fingerprinting techniques, or a router in a multi-protocol label-switched (MPLS) network may not decrement the IP header's TTL for packets on a label-switched path.

If not decrementing the packet's TTL, the device will always forward the packet to the next node. The effect is to omit the non-TTL decrementing device from the Path Visualization graph.

To permit a device to decrement the Time-to-Live field of routed packets, check your device's configuration settings, consult your security administrator or the documentation for the device, or contact technical support for the device's manufacturer.
