# Internet-Aware Synthetic Transaction Monitoring

Monitoring how users interact with your website and baselining critical workflows through synthetic transaction monitoring is not an alien concept. It’s a technique that was developed a long time ago and continues to be a popular choice for application and ITOps/monitoring teams to validate changes and proactively monitor application performance.

The principles of synthetic monitoring, with a strict focus on app-centric performance, have undergone nearly zero change over the past decade. However, the enterprise environment that it monitors has gone through a massive digital transformation. In a world where the digital delivery supply chain has evolved with the cloud, monitoring is still playing catch up. When in-house apps are distributed, interact with multiple third-party services through APIs across multi-cloud environments, and when enterprises are adopting SaaS for mission-critical applications, traditional synthetic monitoring with its app-only focus and no knowledge of underlying dependencies and its influence on application performance is no longer good enough.

The limitations presented by traditional synthetics in a digital transforming enterprise landscape is what motivated us to introduce ThousandEyes Synthetics. ThousandEyes Synthetics with browser synthetic monitoring provides a holistic understanding of end-to-end application or website performance and business transactions with a tight correlation to cloud infrastructure and Internet behavior.

### Introducing ThousandEyes Synthetics

ThousandEyes Synthetics combines the power of synthetic transaction monitoring (including a new, programmable javascript-based approach) with deep active monitoring that correlates synthetic tests with HTTP, network metrics, network path, Internet routing and outage visibility. Time-correlated full-stack visibility in a single dashboard expedites faster root-cause analysis and time to localization of faults and application performance issues in a cloud and Internet-dependent environment.

Figure 1: Map insights from synthetic transaction tests to HTTP availability, response times and see how the underlying network path from users to your website is impacting performance.

### New Transaction Test Type

Access to the new browser monitoring capabilities will be introduced through a new test type called “Transaction.” ThousandEyes Synthetics’ scripted browsers emulate and monitor a customer user experience by scripting browsers that navigate a URL, take specific actions and make sure specific elements are present. The new test type supports JavaScript bindings for the Selenium WebDriver 4.0 that emulates a Chrome browser and walks through each step of the script. The new test type comes with a web-based recorder that easily allows you to craft a user journey, as seen in Figure 2.

Figure 2: A web-based recorder makes it easy to capture multi-step transactions for monitoring purposes

Note: We will continue to support tests built on the older transaction engine, and customers using our current transaction tests will not see any disruption. These older transaction tests will be labeled as “Transaction Classic.”

### So what can you do with ThousandEyes Synthetics?

* Take advantage of the programmability of Javascript-based workflow creation to customize the navigation path, test for asserts and conditionals.
* Define custom markers for critical points in the user journey and record key performance metrics such as total time taken to complete an end-to-end user journey, and time taken to complete each logical business transaction along with successful completion metrics
* Dig into the details of transaction tests, which are a series of page load tests interspersed with synthetic user interactions, like typing in fields and clicking buttons. You can now see how individual objects load across multiple pages, or interactions, and identify bottlenecks
* Play back scripted transactions and save snapshots at customizable intervals to debug failed transactions
* Schedule tests with flexible round-robin scheduling that allows for granular testing up to 1 minute

### Monitor from where your users are, not where your app is located!

No matter whether your application is hosted in a hybrid cloud or is from a SaaS provider, monitoring availability and performance from where your users are (be they human or machine) is critical. Many SaaS, such as Salesforce and collaboration suites, serve employees, customers and partners, which makes both inside-out and outside-in visibility equally important.

An important point to note is that while having monitoring agents in public cloud regions is great for monitoring third-party APIs or remote microservices from workloads running in those clouds, public clouds are highly unrealistic if you try to use them to represent human users. That’s because public cloud networks are so massively, well, networked. You can check out our [2018 Public Cloud Performance Benchmark Report](https://www.thousandeyes.com/research/public-cloud?utm\_source=Blog\&utm\_medium=Textlink) for more details on public cloud network performance, but the point is that if you’re trying to monitor from the vantage point of real users, you need to do it from representative networks.

That’s why ThousandEyes offers layered visibility from transactions down to Internet routing from pre-deployed Cloud Agents in more than 180 cities around the world, including regional data centers of four major cloud providers (AWS, Alibaba Cloud, Azure and GCP), and also from tons of Tier 1, 2, and 3 ISPs and broadband providers. You can also deploy Enterprise Agents in your branch offices, data centers and VPCs.

Unlike some vendors who have withdrawn from offering real user vantage points, or who have never made that investment and have only ever had public cloud vantage points, or who have inconsistent monitoring capabilities depending on the type of agent, ThousandEyes has an unmatched set of vantage points and offers the same in-depth visibility from all those agents. And we’re continuously making new investments in our global fleet of monitoring vantage points.

#### [ThousandEyes customers can see the new transaction test type available in Test Settings. If you’re not yet using ThousandEyes, get started with a free trial today.](https://www.thousandeyes.com/signup?utm\_source=Blog\&utm\_medium=Textlink)
