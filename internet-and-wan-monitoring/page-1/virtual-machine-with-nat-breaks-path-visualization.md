# Virtual Machine with NAT Breaks Path Visualization

ThousandEyes Enterprise Agents are commonly installed in virtual machines, which are run by hypervisor software. Commercially available hypervisor software found on desktop and laptop systems includes VMware Workstation (Windows and Linux operating systems) and VMware Fusion (Mac OS X), and Parallels Desktop (Mac OS X). Additionally, Oracle VirtualBox is freely distributed hypervisor software for all three operating systems. Enterprise Agents are often installed in a virtual machine run by one of these hypervisors.

When a virtual machine's network adapter mode is "NAT" or "NAT Network", the Path Visualization portion of a test will be unable to render the correct number of hops in the path from an Enterprise Agent to a test target, if the test is sending TCP segments outbound. TCP is used for all Path Visualizations except Voice Layer RTP Stream tests and Agent to Agent tests not configured with TCP. NAT, or network address translation, is often used with virtual machines to hide the IP address of guest operating systems behind the host's IP address.

ThousandEyes tests which send ICMP outbound rather than TCP to perform the Path Visualization are unaffected. Also, when the virtual machine's network adapter mode uses the "Bridge" setting instead of a NAT setting, the Path Visualization is unaffected.

The cause of the issue is a limitation in the NAT implementation of these hypervisors. With NAT, the hypervisor fails to preserve the value of the Time to Live (TTL) field in the IP header of packets sent to and from the virtual machine, when the packets use TCP as the transport layer protocol. Instead of preserving the existing TTL, the TTL is reset to either 64 or 255. For example, VirtualBox resets all TTLs to 64 when in NAT mode, and in NAT Network mode, packets from the Agent have TTLs reset to 64 and packets to the Agent have TTLs reset to 255.

Resetting the TTL breaks the standard path trace mechanism of setting TTL = 1 to identify the first hop in the path, TTL = 2 to identify the second hop, and so on.

A ThousandEyes Enterprise Agent performing Path Visualization using TCP sends TCP SYN packets towards the target. With the Agent's network adapter in NAT mode, the first hop (the virtual machine host) will respond to the SYN packet (having a TTL = 1) with an ICMP Time-to-Live exceeded packet. The second SYN packet, with TTL = 2, has the TTL changed to 64, which allows the packet to reach the target instead of expiring on the second hop. A normally functioning target replies with TCP SYN ACK, terminating the trace. Thus, the Path Visualization consists of the Agent, then one hop (the host running the hypervisor) and then the target. Below is a Path Visualization as it would appear from an Agent in Oracle VirtualBox with the "NAT" setting, or in VMware Fusion with the "Share My Mac" setting:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e5a6ceb01de52687769c631ed0f760ffee268e17%2Fproduct-documentation\_advanced-troubleshooting\_virtual-machine-with-nat-breaks-path-visualization-1.png?alt=media)

With the Agent's network adapter set to NAT Network, the first hop (the host) does not respond to the SYN packet (having an original TTL = 1) with an ICMP Time-to-Live exceeded packet, and the first SYN packet has the TTL changed to 64, which allows the packet to reach the target. A normally functioning target replies with TCP SYN ACK, terminating the trace. Thus, the Path Visualization consists of only the Agent and the target. Below is a Path Visualization as it would appear from an Agent in Oracle VirtualBox with the "NAT Network" setting, or in Parallels with the "Shared Network" setting:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dc2d1f475ca2f0dc2657dd99716048a34fbfa10b%2Fproduct-documentation\_advanced-troubleshooting\_virtual-machine-with-nat-breaks-path-visualization-2.png?alt=media)

The limitation is best documented in the Networking chapter of the VirtualBox user's guide, in the section

[NAT Limitations](https://www.virtualbox.org/manual/ch06.html#nat-limitations)

:

Some frequently used network debugging tools (e.g. ping or tracerouting) rely on the ICMP protocol for sending/receiving messages. While ICMP support has been improved with VirtualBox 2.1 (ping should now work), some other tools may not work reliably.

A bug ticket for the issue can be found at:

Other hypervisor documentation is sparse, but the VWware communities site contains the following thread:

Given the length of time which this limitation has been present in these products, a solution is unlikely to be provided by the vendors.

The preferred work-around for this issue is to set the virtual machine's network adapter mode to "Bridged". If a bridged adapter is not possible, for example due to IP address assignment limitations on the local area network, then an alternative to performing NAT via the hypervisor is to perform NAT using the host's native operating system functionality.

For example, a host running a Microsoft operating system could provide NAT through Windows Internet Connection Sharing. On Mac OS X, the Sharing preference under System Preferences provides an "Internet Sharing" option. Typically, these methods would be used with the virtual machine's network adapter in "Host-Only" mode. Note, however, that ThousandEyes Customer Engineering has not found a configuration which will work using this method, at this time.

We have had limited success when running Mac OS X using the

[pf](https://www.openbsd.org/faq/pf/)

utility to set up the required NAT rules, with the limitation that the ICMP Time-to-Live exceeded packets (ICMP type 11) do not reach the Enterprise Agent guest, resulting in a Path Visualization which has only "white nodes" (nodes with no information, such as IP address) on the path between the Agent and the target. A configuration which would be used in the

[pf.conf](https://man.openbsd.org/pf.conf.5)

file

nat on en1 from 192.168.56.0/24 to any

pass from {lo0, 192.168.56.0/24} to any

This configuration performs NAT for any virtual machine on the virtual network 192.168.56.0/24 (first line) and then allows the traffic out (second line).
