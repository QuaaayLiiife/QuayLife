# Browser Synthetics Test Types

ThousandEyes Browser Synthetics includes two test types: transaction tests and page load tests.

* **Page load tests** access a single page from a target URL, and measure the time it takes each page element to load. They also measure the timing of the DOM and page load events, and other metrics.
* **Transaction tests** simulate complex user journeys such as browsing an online shopping site and making a purchase. Transaction tests provide page load metrics for multiple pages instead of a single page. You can also use the scripting feature of transaction tests to make API calls.

Both page load and transaction tests include lower-level network tests already built in. For example, you’ll see the same network views as you would for an agent-to-server test.
