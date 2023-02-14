# Automated Session Tests

Automated Session Tests enable the Endpoint Agent to monitor and identify network connections between a user’s application and the destination node (host server); thereby, removing the ambiguity of knowing whether the IP addresses created in synthetic tests are going to the right datacentre or service.

Automated Session Tests capture the performance of a desktop application without you having to manually configure an IP address or hostname for the application. These tests are the same as Agent-to-Server Scheduled Tests, however ThousandEyes determines which endpoints to monitor.

#### Advantages of using Automated Session Tests <a href="#advantages-of-using-automated-session-tests" id="advantages-of-using-automated-session-tests"></a>

In comparison to Scheduled Tests, the Automated Session Tests provide the following advantages:

* The tests execute only when the application is used, which in turn optimizes the system and network resources.
* If a user changes their location or connection, resulting in the application connecting to a different IP address, the dynamic nature of these tests would automatically stop testing the old IP address and test a new one.
* These tests enhance user experience as they provide end-to-end visibility to the exact nodes the user's application is connecting to, requiring no on-going configuration to keep tests up to date.
