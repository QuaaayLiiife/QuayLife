# Dynamic Baselines

Dynamic baselines allow users to create alert rules that more accurately reflect the natural variance in test data. Using standard deviation, percentage change, or absolute values, you can configure alert rules that dynamically determine whether to fire or not, based on the historical data of a specific test.

**Note:** Dynamic baselines are currently only available for Cloud and Enterprise Agent alerts.

### 24-Hour Window for Dynamic Baselines <a href="#24-hour-window-for-dynamic-baselines" id="24-hour-window-for-dynamic-baselines"></a>

When you configure an alert rule that uses a dynamic baseline in its alert conditions, the ThousandEyes platform looks back at at 24-hour window to determine the baseline of a specific metric.

With a 24-hour window, the baseline for the metric is based on _at least_ 24 data points (24 hours \* 1-hour test interval). This ensures that alerts are triggered by a valid deviation from a reliable baseline. For additional accuracy, the baseline is updated every 5 minutes, to accommodate any new data from new test rounds.

#### 3-Hour Window for Standard Deviation Dynamic Baselines <a href="#3-hour-window-for-standard-deviation-dynamic-baselines" id="3-hour-window-for-standard-deviation-dynamic-baselines"></a>

When your dynamic baseline is calculated based on a standard deviation, the ThousandEyes platform looks back at a 3-hour window. (The average baseline is still based on the 24-hour window.) This is to ensure that any deviation from the mean is in line with the most recent data points and mitigates the risk of an extremely steady standard deviation over a 24-hour period, which would prevent an alert from firing that might be of interest to our customers.

Let's imagine a scenario where an HTTP server test runs every ten minutes. Over the course of 24 hours, an agent in New York runs the test 144 times. The test gathers response times with an average of 500ms.

Attached to this test is an alert rule that uses a dynamic baseline. Based on the results so far, whether an alert will fire or not for the next test round depends on whether it was configured using standard deviation, percentage change, or an absolute value:

* **Standard deviation** - Say that the standard deviation for last 3 hours' results is 36. Using the default multiplier of 2, the alert will fire if the next test round returns a response time greater than 500+(36x2) = 572ms.
* **Percentage change** - Using the default percentage change of 20%, the alert will fire if the next test round returns a response time greater than 500+20% = 600ms.
* **Absolute value** - Using the default absolute value of 50ms, the alert will fire if the next test round returns a response time of 500+50 = 550ms.

The different options allow you to adapt your alerting framework to better reflect the fluctuation in test results, and ensure that your system isn’t overwhelmed with alerts because of static metric baselines.

### Metrics for Dynamic Baselines <a href="#metrics-for-dynamic-baselines" id="metrics-for-dynamic-baselines"></a>

Dynamic baselines are currently supported for the following metrics:

| Alert Type                | Metric                 |
| ------------------------- | ---------------------- |
| DNS - DNS server          | Resolution time        |
| Network – Agent-to-agent  | Jitter                 |
| Network - Agent-to-agent  | Latency                |
| Network – Agent-to-server | Jitter                 |
| Network - Agent-to-server | Latency                |
| Network – Agent-to-server | Proxy jitter           |
| Network – Agent-to-server | Proxy latency          |
| Voice - RTP stream        | Latency                |
| Voice – RTP Stream        | Packet delay variation |
| Voice – SIP server        | Connect time           |
| Voice - SIP server        | DNS time               |
| Voice – SIP server        | Invite time            |
| Voice – SIP server        | Options time           |
| Voice – SIP server        | Register time          |
| Voice – SIP server        | Response time          |
| Voice - SIP server        | Total time             |
| Voice – SIP server        | Wait time              |
| Web – FTP Server          | Connect time           |
| Web - FTP server          | DNS time               |
| Web – FTP Server          | FTP negotiation time   |
| Web – FTP Server          | Response time          |
| Web - FTP server          | SSL negotiation time   |
| Web - FTP server          | Total time             |
| Web – FTP Server          | Transfer time          |
| Web – FTP Server          | Wait time              |
| Web - HTTP server         | Connect time           |
| Web - HTTP server         | DNS time               |
| Web - HTTP server         | Receive time           |
| Web - HTTP server         | Response time          |
| Web - HTTP server         | SSL negotiation time   |
| Web - HTTP server         | Total time             |
| Web - HTTP server         | Wait time              |
| Web - Page Load           | DOM load time          |
| Web - Page load           | Page load time         |
| Web - Page load           | Response time          |
| Web - Transaction         | Transaction time       |

### Creating Alert Rules with Dynamic Baselines <a href="#creating-alert-rules-with-dynamic-baselines" id="creating-alert-rules-with-dynamic-baselines"></a>

The image below shows an example alert rule that uses a dynamic baseline. The alert rule condition states that if, within the last 24 hours' average, the response time exceeds the last 3 hours' standard deviations by a factor of 2, the alert will fire.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e80e6c52af77832158ebaebd30e5b9cb641ea26e%2Falerts\_dynamic-baselines-1.png?alt=media)

### Inspecting Alerts Triggered by a Dynamic Baseline <a href="#inspecting-alerts-triggered-by-a-dynamic-baseline" id="inspecting-alerts-triggered-by-a-dynamic-baseline"></a>

When an alert is triggered based on a dynamic-baseline alert rule, you can inspect the dynamic baseline used. In the ThousandEyes platform, go to **Alerts > Alert List**. On the **Active Alerts** or **Alert History** tab, hover over the tooltip to see information about the alert rule that generated this alert.

### Mitigating Noisy Dynamic Baseline Alerts <a href="#mitigating-noisy-dynamic-baseline-alerts" id="mitigating-noisy-dynamic-baseline-alerts"></a>

Dynamic baseline alerts that are based on standard deviation can be very "noisy" for metrics with a small or very stable average. For example, the standard deviation of latency for a service could be less than 1ms. If your service jumped from 20ms to 20.4ms, this isn't inherently cause for concern, but if you have configured a sensitive dynamic baseline alert rule, alerts could fire regularly and increase noise.

When you configure an alert rule with a standard deviation-based dynamic baseline condition, we recommend that you add to the alert rule an additional alert condition with an absolute difference from average. For example, you can add a condition that says `latency > 5ms above the mean`. This will ensure that your alert rule will only fire if it is above the standard deviation _and_ above a certain absolute threshold compared to your average.
