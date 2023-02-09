# Webex Cloud Agents

ThousandEyes has Webex-specific Cloud Agents deployed at the front door of several Webex data centers responsible for serving customer traffic. These agents are available for general use by all ThousandEyes customers and are a tool to better monitor and troubleshoot your Webex performance. For more information about the key value of these agents, see

[the Webex Monitoring solution page](https://www.thousandeyes.com/solutions/webex-monitoring)

.

Cloud Agents that are Webex-specific display the Webex icon, and are identified as such in parentheses after the location name, as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-498c238cd2ad45d0c0fc4cad61c7e85a71a93eef%2Fwebex-cloud-agents-labels.png?alt=media)

There are a few key differences between these Webex Cloud Agents and our general Cloud Agents you see on the ThousandEyes platform:

* Most importantly, these agents can only be used as _test targets_ and cannot be the source of any tests. This means that these agents **can only be used in agent-to-agent and RTP stream tests, and only as the target of that test**.
* These agents can perform bidirectional testing, but only after they are selected as a target for the test.
* You can use the Webex Cloud Agents only with other IPv4 agents. IPv6 testing is not supported with the Webex Cloud Agents.

### Webex Cloud Agent Locations <a href="#webex-cloud-agent-locations" id="webex-cloud-agent-locations"></a>
