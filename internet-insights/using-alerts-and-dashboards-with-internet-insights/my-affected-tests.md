# My Affected Tests

An affected test is one that is indirectly impacted, or could potentially be impacted, by an outage elsewhere. A test can be identified as affected even if that test isn’t directly impacted, meaning it is not showing any obvious errors or triggering alerts. In other words, Internet Insights data correlation shows potential impact to your own tests even if your standard monitoring thresholds have not been exceeded.

Affected tests include any test within your organization. This includes tests owned by other account groups. As stated on

[Using Alerts and Dashboards](broken-reference)

, you can see affected tests in several areas on the platform. This section explains how tests are determined to be “affected”.

Other entities can also be determined to be affected, such as domains, servers, networks, errors, or locations.

### Why Are Affected Tests Important? <a href="#why-are-affected-tests-important" id="why-are-affected-tests-important"></a>

Your tests focus on specific outages that _you_ care about. Even if you don’t care about every single global Internet outage, there’s always the potential for a cascading series of outages that could eventually affect your operations. The interdependent nature of the Internet means that the root cause of an outage could be very different from initial observations about that outage.

Internet Insights makes inferences about global outages that involve the same targets that you’re testing to, even if your own tests aren’t showing errors.

### Linking Affected Tests to Alerts and Dashboards <a href="#linking-affected-tests-to-alerts-and-dashboards" id="linking-affected-tests-to-alerts-and-dashboards"></a>

You can link up affected tests to alerts and dashboards as follows:

* In **Dashboards**, you can configure a custom dashboard using the Map widget to display metrics for your affected tests on a global map.

### Use Case Example for Affected Tests <a href="#use-case-example-for-affected-tests" id="use-case-example-for-affected-tests"></a>

Here is an example of why an Internet Insights subscriber might care about a global Internet outage, even when their own tests aren’t showing errors, and their own systems seem to be working normally.

Suppose that you are a ridesharing company that has greater presence in some cities than others. Your test is monitoring a particular application target running in an Amazon Web Services data center located in Europe, a single instance that services all worldwide customers from that one location.

This target needs to be 100% available from anywhere in the world. If it’s not reachable, or isn’t reachable from certain regions, your operations in certain cities could stop working, leading to loss of revenue and confidence. Customers and investors alike could switch allegiance. Given that most of your customers are in the U.S., you’ve chosen to run this test only from ThousandEyes agents in the U.S. because it’s more cost-effective. However, 5% of your customers are in Australia.

You have selected Internet Insights packages to ensure combined coverage of all global ISPs. So you’ll see ISP outages in Australia on the Internet Insights Overview map, even though you’re not running any of your own tests from agents located in Australia.

On a particular date, Internet Insights detects a global outage that affects a portion of the network path from Australia to the same application target in Europe that you’re monitoring from the U.S. Other ThousandEyes customers happen to be running similar tests to the same application target from agents located elsewhere in the world, including Australia, and it’s the ThousandEyes agents located in Australia that are reporting problems with reaching this particular European target.

So why, or when, would this matter for our hypothetical ridesharing company? The graphic below shows how interrelated tests could influence each other.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-73df4874abcd460b2f633d178a2ccb00f69e1301%2Fmy-affected-tests-reroute-example-001.png?alt=media)

You can use this information to take proactive measures, for example:

* During this particular outage, you have customers in Australia who might be having issues connecting to your app or your service.
* The “affected tests” Dashboard widgets highlight visibility into an outage that affects targets you’re already monitoring. You’ll be aware of any real issues sooner, which can help you reach out to your customers or alert your local network teams for further action.
* You can set up an alert with notifications to your local network teams so that they’re aware of the situation without your direct involvement.
* You can embed any of the Dashboard widgets in other web applications, so that your local network teams have access to data in a visual form.
* If the outage spreads, it could begin to impact your customers in other places. For example, traffic from the U.S. could get re-routed through a trouble spot. With better visibility, you can be more proactive about mitigation.
