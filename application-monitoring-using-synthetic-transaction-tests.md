# Application Monitoring using Synthetic Transaction Tests

Today, we released our new [synthetic transaction](https://www.thousandeyes.com/solutions/browser-synthetic-monitoring?utm\_source=Blog\&utm\_medium=Textlink) capabilities for application monitoring to full general availability. Our new Selenium WebDriver based synthetic transaction tests are 100% native Javascript and use Chromium browser for recording and execution, allowing you to create more accurate, flexible and consistent synthetic application tests. We make this accessible to all users with an easy-to-use Recorder that also doubles as a Javascript IDE, so you can start fast and build detailed user workflows. And with complete API support for synthetics, you can better automate and integrate transaction tests into your CI/CD processes.

### How to Get the Most Out of the New Transaction Test

In this blog, we'll take a closer look at our [new synthetics capabilities](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA02R000000UIOMSA4\_Getting-started-with-transactions?utm\_source=Blog\&utm\_medium=Textlink) using Office 365 Sharepoint as an example. We'll show how you can get started fast and recommend some key best practices for creating powerful, cross-correlated synthetic app and network monitoring tests for better visibility into today's cloud and SaaS applications.

#### #1: Think Workflow, Not Clicks

First off, when creating a transaction test, you want to focus on targeting common end-user workflows. This is in contrast to "clicking around"; the goal of synthetic application monitoring is not to click on every link and make sure every button is working. (That's the job of your QA team.) That's not to say that ThousandEyes can't be used in a CI/CD process—it can and should. But the goal here is to replicate common end-to-end user workflows so that you can identify when users may be having a degraded digital experience.

So with that in mind, start by identifying some key end-user workflows you want to target. In this example, we'll target a common user flow: downloading a file from Sharepoint. The user flow will be something like this:

_Browse to Sharepoint Online --> Login --> Browse to Documents Page --> Select Document --> Download_

Creating common end-to-end user flows will ensure that you're exercising all the infrastructure and interconnected services that make up your application and that can impact end-user digital experience.

#### #2: Don't Fear the Javascript—Start with the Recorder

Having a native Javascript-based transaction engine is the best way to create robust and reliable transaction scripts. While UI-based solutions may seem easier, when something doesn't work, you’re generally stuck. Native Javascript provides flexibility and power to make adjustments where needed.

However, Javascript may be a bit unfamiliar for some. If that's you, use the ThousandEyes Recorder to get started quickly. The ThousandEyes Recorder is a standalone transaction script recorder and IDE that will intelligently generate all the necessary Javascript code based on your web interactions. Using our Office 365 Sharepoint workflow as an example, we can start by pasting in the target URL ("https://...") into the built-in Chromium browser, clicking record, interacting with the website according to our user workflow, and clicking "Stop" when done. The Recorder will then create a complete Javascript transaction based on our recorded user actions (Figure 1).

Figure 1: ThousandEyes Recorder auto generates a complete transaction script

The Recorder creates human readable text comments, making it easy for Javascript first-timers to quickly understand what each line of code is actually doing. For example, here's one of the snippets from our Sharepoint transaction script where we're entering our login information:

_\`// Click on 'Enter your email, phone, or Skype.'_\
_await click(By.id('i0116')); // Clicking the text field_\
_await typeText('marketing@ThousandEyesO365.onmicrosoft.com', By.id('i0116'));\`_

It also automatically captures passwords and adds them to the built-in credential store, which are easily accessible using \`credentials.get\`. The credential store (Figure 2) is a secure secrets repository that can be used to enter passwords without having to use as plain text in transaction scripts, which can be a major security concern.

Figure 2: ThousandEyes Recorder automatically captures and stores credentials

Finally, the ThousandEyes Recorder generates all the required scaffolding code ("imports", etc.) as well as a number of helpful functions like "click", "typeText", "isElementClickable", "simulateHumanDelay" and others that can be used to make it easier to create reliable and robust transaction scripts.

#### #3: Embrace the Javascript (and Keep Using the Recorder)

While the Recorder is a great tool for getting started quickly, you'll want to get your hands dirty and embrace the power of Javascript as soon as possible. To support this, the ThousandEyes Recorder also functions as an IDE (Integrated Development Environment), with helpful tools like syntax error highlighting, intellisense, autocomplete, console output for debugging and more.

One of the most effective ways to make your transaction code more reliable and robust is to modify the means by which your transaction script finds elements on the webpage. By default, the Recorder uses an element's ID, if it has one. For example, the code below from our generated Office 365 transaction script identifies an element on the page with ID \`idSIDButton9\` (Figure 3).

Figure 3: Element on page with ID idSIDButton9

This approach is typically a best practice as IDs are generally unique. But with today's dynamic web pages, IDs can sometimes change with each page load. Alternative selection methods include: constructing a unique CSS selection string, element name, element class, element linkText and others.

In our Office 365 Sharepoint example, running the recorded transaction periodically generates an error that element "id\_354" (the Download button) can't be found (Figure 4). This is because the element ID is dynamically generated on each page load.

Figure 4: Getting your hands dirty: changing the element selector method

Using Chrome dev tools (right click "Inspect") on the built in Chromium browser, we can look for a better selector for the "download" button (Figure 5). In our Sharepoint example, we can see the Download button has an image with an attribute: \`data-icon-name="download"\`. This is a good example of a reliable identifier as the name "download" is likely unique and unlikely to change dynamically.

Figure 5: Using Chrome dev tools to find a better selector

Replacing \`await click(By.id('id\_\_354'));\` with \`await click (By.css('\[data-icon-name="download"]'));\` and re-running the modified transaction script right within the ThousandEyes Recorder solves the problem and allows our script to run repeatedly with no issues.

Identifying the right CSS and other selectors is one of the most powerful ways to create robust transaction scripts. The following [cheat sheet](https://www.red-gate.com/simple-talk/wp-content/uploads/imported/1269-Locators\_table\_1\_0\_2.pdf?file=4937) from Red Gate is great to have on hand to remember common selector recipes.

Modifying the selection scripts is just one way you can get your hands dirty and leverage the power of Javascript.

Another example of leveraging the power of a Javascript-native engine is to use some of the built-in helper functions provided by ThousandEyes. For example, we'll want to use the \`downloads.waitForDownload (...)\` function in our Sharepoint example to wait for the file selected for download to actually complete. To do this, we'll just need to import the \`download\` module and add the call at the end of our script. Here's a code snippet:

_\`import { downloads } from 'thousandeyes';\`_\
_..._\
_\`// Click on 'Download'_\
_await click(By.css(\[data-icon-name="download"]));_\
_// Wait for download to complete_\
_await downloads.waitForDownload('Public Cloud Report.pdf', 60 \* 1000);\`_

As you tweak and refine your code, you can replay your transaction script directly from the recorder, so you can make sure everything is working as expected. This is why a native Javascript approach is important, because unlike other tools, ThousandEyes is able to execute your transaction scripts verbatim across all Cloud and Enterprise agents. So you can be confident the behavior will be consistent and what you expect.

#### #4: Leverage Markers for Better Digital Experience Visibility

One of the challenges with measuring end-user digital experience is that issues can crop up in any number of places within a typical user workflow. Markers are used to identify and measure key tasks within a workflow so that you can take action if any single task takes too long. They can be added using the marker icon, or \`driver.start\`/\`driver.stop\`.

Properly setting up markers is one of the most important steps in creating a helpful transaction script. Adding too many markers prevents creating meaningful performance triggers (too much noise) while adding too few risks losing the ability to measure important sub-steps within a typical user workflow.

Some common markers you'll want to consider creating are:

* "Page Load"—Create a marker around the initial \`await driver.get\` call so that you can measure the initial page load time of the site
* "Login"—Start a marker after initial page load and stop the marker after the final login (password) button click.
* "Backend"—Create a marker that starts after any login occurs and ends when the page is loaded/final user action is complete.
* Create markers for other common user actions relevant to how the application is used. For instance, in our Sharepoint Download example, we might create a marker around the user action of searching for and downloading a file, since that's a common way Sharepoint is used.

Figure 6: Leveraging markers to gain more granular digital experience measurements

A helpful tip regarding markers is that, by default, when an event like a user 'click' results in a page load, the event won't return until the page is loaded, which may lead to unexpected marker timings. The Sharepoint Login is one such example. Luckily, because we're using Javascript, we can easily adjust the code to wait until \`isElementClickable()\`, stop our "Login" marker, start our "Backend Load" marker, and only then proceed to call \`click()\`.

Once you have markers in place, you can create alerts on specific markers. For example, we might want to create an alert if the "Backend Page Load" takes too long.

#### #5: Employ Screenshots for Faster Troubleshooting

Another best practice is to leverage screenshots to periodically capture what an end user is experiencing. Doing so allows faster identification of issues and better understanding of web behavior. ThousandEyes Synthetics allows screenshots to be taken anywhere in the transaction script by calling \`await driver.takeScreenshot();\` (or by clicking the screenshot icon), which will generate a screenshot that is the same as what the end user would see.

A strongly suggested practice is to take a screenshot immediately after the initial page load. This ensures that you'll always have a visual record of what the end user is seeing immediately after they login (i.e. their initial experience with a service). This can be of huge help in quickly remediating issues.

For example, in the October 2019 PG\&E website outage, a simple transaction test with a screenshot quickly identified that an SSL configuration issue was preventing users from establishing HTTPS connections with their site.

In addition, the ThousandEyes Synthetics engine will also automatically generate a screenshot whenever a transaction error or timeout occurs. This is hugely valuable for quickly resolving problems and optimizing transaction script behavior.

For example, our "Sharepoint" transaction script was periodically experiencing timeouts. Looking at the automatically captured screenshot indicated that an unexpected popup was occurring that was not handled by our script (Figure 7).

Figure 7: Automatically captured screenshot reveals an unexpected popup

This would have been practically impossible to glean from waterfall information. Armed with this data, we can easily update our transaction code to check for this popup and handle it if needed.

These are just a few examples of why screenshots are more than just pretty pictures but valuable tools in your digital experience monitoring toolkit.

#### #6: Go Beyond the Recorder: Building a Library of Code

The ThousandEyes Recorder is an awesome tool that makes it easy to get started creating powerful transaction scripts. However, you don't want to always reinvent the wheel. Once you've started building transaction tests, you'll want to start reusing common code across your teams. Creating a library of common functions for users across your team to leverage and re-use will allow you to more quickly build reliable and powerful transaction tests.

For example, you may want to create reusable functions for common user flow snippets for your website, like logging in, browsing from the home page to key end user portals on your site, etc. You may also want to start creating a library of lower-level helper functions, like retrying clicks, closing random popups, etc.

In fact—we've already started this for you. Check out our [transactions examples](https://github.com/thousandeyes/transaction-scripting-examples) on GitHub, which include many examples like using credentials, waiting for a file to download, switching between tabs, closing popups and more (Figure 8).

Figure 8: ThousandEyes transaction code examples on GitHub

Taking this kind of modular approach allows more developer-oriented team members to focus on building, testing and optimizing reusable code while less dev-oriented members can focus on building higher-order transaction scripts.

It also sets you up for following the best practice of versioning your transaction scripts in a repository like GitHub, just like you do all your other application code. Furthermore, the ThousandEyes API allows you to dynamically update your transaction test scripts so you can integrate everything with your existing CI/CD processes.

When we're satisfied with our transaction script, we can easily export it from the Recorder directly into ThousandEyes.

#### #7: Handle SSO Like a Champ

At this point, we have a fully functioning Office 365 Sharepoint transaction test that follows a typical user flow of loading Sharepoint, logging in, browsing to a shared documents folder, and downloading a file. However, if you're a large enterprise, it's very likely you're using some form of Single Sign On (SSO). This can be a road-block for transaction testing. In some cases, your SSO provider will redirect you to an interactive login for, which you'll simply handle in the transaction test just like any other login. In others, your provider may require Kerberos or NTLM. Luckily, ThousandEyes can handle this automatically. You just need to add your credentials to the "Auth Settings" section of the transaction test setup.

Once your credentials are added, the ThousandEyes synthetics engine will handle the SSO authentication automatically. Not only does this avoid having to add special SSO related code, it also keeps your transaction script more representative of the end-user transaction steps.

#### #8: Combine Network and Application Synthetics for Better Insights

With our new Office 365 transaction test up and running in ThousandEyes, we'll quickly start to see the benefits of correlating application synthetics with full end-to-end network and Internet visibility.

As a real-world example, we ran our Sharepoint transaction test from multiple North America vantage points and quickly identified a not-so-obvious network issue impacting end-user application performance. While the initial page load time didn't show any issues, the marker time for loading the Sharepoint "shared documents" page was twice as long for Boston locations as other locations (Figure 9). A non-transaction based test or waterfall analysis would not have identified this issue.

This is a perfect example of why we highly recommend having even simple transaction tests running against your key applications.

Figure 9: Sharepoint slow application performance from Boston region

With a traditional synthetics tool, we'd be stuck at this point, perhaps left to call a cross-functional meeting with eng, IT ops and NetOps. However, with ThousandEyes' fully correlated network metrics and end-to-end path visualization, we quickly identified that network latency related to sub-optimal routing to Microsoft's edge network in the Boston region was a key contributor to the delays (Figure 10).

Figure 10: Boston traffic to Office 365 is routed through New York, contributing to 10x latency

It's important to note that the detected network latency would typically not have been enough to trigger an alert. This is a great example of why having application and network visibility work in concert is so critical when it comes to ensuring optimal digital experience of today's cloud and SaaS-based applications. We'll discuss this and other examples in greater detail in a follow-up blog on how network latency and cloud edge architectures can impact SaaS and cloud application performance.

### Wrapping Up

In this blog, we learned how quickly we can get started creating Javascript-native transaction tests using the ThousandEyes recorder. We tweaked the code with some best practice optimizations, leveraged some built-in libraries to add functionality like downloading a file, added markers and screenshots, and finally saw the benefits of bringing together application and network visibility under one common, correlated test.

#### [If you’re already a ThousandEyes customer, you’ll see the new transaction test type available in Test Settings. If you’re not yet using ThousandEyes, get started with a free trial today.](https://www.thousandeyes.com/signup?utm\_source=Blog\&utm\_medium=Textlink)
