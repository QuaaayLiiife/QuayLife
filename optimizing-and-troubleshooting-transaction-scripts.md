# Optimizing and Troubleshooting Transaction Scripts

This article describes some basic optimizations, some of which are also important for troubleshooting during script development. See

[Upgrading to BrowserBot 2.6+ (Chromium 97)](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/upgrading-to-browserbot-26)

for more information on recent BrowserBot upgrades that might impact your existing transaction scripts.

### Use the Correct Window Size <a href="#use-the-correct-window-size" id="use-the-correct-window-size"></a>

When using the Recorder to generate a new transaction script, set the window size chosen in the **Start Recording** dialog to match your actual window size. For example, if you are using a widescreen monitor to interact with a web site, then you would select "Desktop Large" or "Desktop Extra Large".

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3a3af643d2b3b43b598c73dc30e6036af5583129%2Foptimizing-transaction-scripts-001-start-recording-set-window-size.png?alt=media)

You can use start and stop markers to capture the timing for any user workflow or business transaction, for example Add to Cart, Submit Order, or a custom back-end query. The workflow timing will be called out on the **Waterfall** tab for the transaction test view.

You can use custom marker timings as a metric when configuring transaction test alert rules. Marker timing is also available as a metric on many of the Cloud & Enterprise Agents dashboard widgets as well.

Markers are useful in several ways:

* Identify where a script section starts and stops.
* Identify when a process takes longer than expected.
* By comparing a marker against an Agent’s waterfall, you can also verify that the page finished loading before the `marker.stop()` entry.

Steps to add markers to your script:

1.  1\.

    Include "markers" in the **thousandeyes** import line at the top of the script:

    import { driver, browser, credentials, markers } from 'thousandeyes';
2.  2\.

    Within your script, add markers to delineate between the beginning and ending of each step. For example, to add timings for displaying a particular navigation menu:

    markers.start('Navigate menu');

    markers.stop('Navigate menu');

The Selenium webdriver used by the ThousandEyes browser synthetics testing feature waits for a page or frame load if a `click()` triggers a new page load. This can result in inaccurate marker timings unless you start the new marker before the click, as shown below:

// More accurate markers at click()

async function markerClick (selector, markerStop, markerStart) {

await driver.findElement(selector);

await markers.stop (markerStop);

await markers.start(markerStart);

### Use Screenshots for Troubleshooting <a href="#use-screenshots-for-troubleshooting" id="use-screenshots-for-troubleshooting"></a>

Although screenshots add time to a script, they are also useful troubleshooting tools during script development. Generally, you can use screenshots when you need to know the state of the screen before an action takes place.

Consider the following guidelines:

Don’t include screenshots within markers, as that will skew the marker timings. Use screenshots selectively in the final script, as they add time.

Add this line to your script to take a screenshot:

await driver.takeScreenshot();

### Choose the Right Element Identifiers <a href="#choose-the-right-element-identifiers" id="choose-the-right-element-identifiers"></a>

By default, the ThousandEyes Recorder uses CSS identifiers to locate HTML page elements. If you run into issues, for example you see errors in the test view on the ThousandEyes platform saying “unable to locate target element”, try using your browser’s developer tools to look for the XPath of the target element. (XPath is a query language for selecting nodes from an XML document.)

Below is example of a simple use of XPath:

await click(By.xpath(\`//\*\[@id="l\_id1:impPost1"]/div/div\[3]/input\[1]\`));

### Use Sleeps and Human Delay Sparingly <a href="#use-sleeps-and-human-delay-sparingly" id="use-sleeps-and-human-delay-sparingly"></a>

All steps involving web page elements have implicit waiting conditions. For example, `click(By.xpath('//button'))` implicitly waits for the `//button` element to be present. When a transaction is recorded in the ThousandEyes Recorder, this implicit timeout setting is always set to 7 seconds by default. If you need to check for a specific element state, you can use `until ()`. See

[Waiting for Element State](https://github.com/thousandeyes/docs/blob/prod/product-documentation/browser-synthetics/transaction-tests/development-guide/robust-transaction-scripts/product-documentation/browser-synthetics/transaction-tests/development-guide/creating-robust-transaction-scripts/transaction-scripting-tips/README.md#waiting-for-element-state)

for examples.

Increasing the human delay, and adding sleeps, are great tools during troubleshooting but they pose two issues: skewed marker times, and increased time to completion. The advice is to use these tools during script development, and then remove them or do other fine-tuning before deploying the ThousandEyes transaction test in a production environment.

Once you have a script working using the JavaScript `sleep()` function, you can shave off time by minimizing sleeps, and by keeping the human delay at 550ms, which is the inherent or default behavior. Any additional waits should be done via conditionals or sleeps. Note that you do not need to import `sleep()` in order to use it.

If you must pause in order to wait for an element to be visible, or to be in a specific state, you can import `until()` from the selenium-webdriver library, and then use a 'wait for condition' command similar to the ones described in

[Waiting for Events](broken-reference)

.

You can import `until()` from selenium-webdriver as follows:

import { By, Key, until } from 'selenium-webdriver';

Below is an example of a simple “wait until” condition, which is making sure that the specified page element has actually been rendered and can be interacted with, vs. when it first appears in the Document Object Model (DOM).

await driver.wait(until.titleIs('webdriver - Google Search'), 1000);

An example of adding a sleep for 1 second is as follows:

await driver.sleep(1000);

Remember to use sleeps mainly during development, but only sparingly in production.
