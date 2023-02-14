# Cloud Agent with Local Problems

When a Cloud Agent experiences full or partial loss of network connectivity or other problems affecting the agent's ability to perform tests, the agent is marked with a "Local Problems" error message on the test results page. Typically, such problems occur due to provider issues, such as server or network hardware failures, or network errors such as routing or other configuration errors.

On the Timeline, a grey bar indicates the rounds when the test used one or more Cloud Agents with a local problem (see the red box in the screenshot below). Hovering over the bar will display a tooltip, indicating which agent(s) are affected. Additionally, the "Local Problems" error message appears in tooltips when hovering over the agent name in the Tables tab or hovering over the agent icon in the Path Visualization.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ef5396284386f59b60343db229ee5391f9bd5daf%2Fproduct-documentation\_tests\_cloud-agent-with-local-problems-1.png?alt=media)

The ThousandEyes Operations team runs agent-to-agent tests to all Cloud Agent sites to determine agent reachability. The "Local Problems" error indicates that at least 80% of the testing agents received unsatisfactory results from the agent-to-agent tests for at least two consecutive rounds of testing.

Agents marked with the "Local Problems" error message may continue to provide data. Any data will be shown in the test results and will contribute to metrics which are averages across all agents. Similarly, the data will be used in Alerts and Reports.

However, an agent displaying the "Local Problems" error will not be counted in the Alert Conditions calculations of an Alert Rule. For example, consider an HTTP Server test run by two agents, with an Alert Rule having the Alert Condition of "All conditions are met by at least 2 agents" for Response Time:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8b33bc23d5f45e46a974f1351bc091e6524866bb%2Fproduct-documentation\_tests\_cloud-agent-with-local-problems-2.png?alt=media)

If one or both agents are marked with the "Local Problems" error then this condition will never be met because the total number of agents used in the calculation will be fewer than two, even if the agent(s) marked with local problems can provide Response Time data and the Response Time from both agents is greater than 100 ms.

Generally, tests with fewer agents will be more likely to miss an Alert Rule condition when an agent has local problems. Consider using multiple Alert Rules that are met by different agent values in the conditions (perhaps with different Notifications characteristics) for tests run by small numbers of Cloud Agents.
