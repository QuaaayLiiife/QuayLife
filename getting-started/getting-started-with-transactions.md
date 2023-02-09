# Getting Started with Transactions

ThousandEyes transaction tests are Web layer tests similar to HTTP server tests and page load tests, except that transaction tests can interact with their targets in order to mimic multi-step user journeys or API sequences. Transaction tests provide greater insight into user experience, and enable you to ensure that those user journeys complete successfully.

Compare these three web layer test types below:

|                                                                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The ThousandEyes Cloud or Enterprise Agent sends a single request and expects a single valid response. Measures response time and validates the HTTP status code to compute server availability. HTTP server tests are used to monitor web servers to ensure they are available and performant. | ThousandEyes agent runs Chromium in order to request and render a single web page. Chromium sends an initial request for the page, then renders the response, and iteratively requests all of the components within the page, including images, JavaScript files, CSS, and AJAX requests. Page load tests monitor the web server that serves the page and all of the page's dependencies. A page load test can be thought of as multiple HTTP server tests combined in one. | <p><em>Browser Synthetics</em>: Agent runs Chromium which is automatically driven by a Selenium script. The script can navigate through multiple pages and interact with them. A browser synthetics transaction test can be thought of as multiple page load tests combined in one.</p><p><em>API Monitoring</em>: Agent runs a script in <code>Node.js</code> to sequentially or iteratively make arbitrary API requests towards the target using the <code>node-fetch</code> library.</p> |

#### When to Use a Transaction Test <a href="#when-to-use-a-transaction-test" id="when-to-use-a-transaction-test"></a>

Transaction tests measure web user experience using either synthetic browser interactions, or sequences of API requests. Transaction tests should be used for testing _multi-step workflows_. This type of test can uncover problems that aren't always apparent from loading a single page, as with a page load test, or sending a single request, as with an HTTP server test. For example, if your app or web site relies on returning customer data from somewhere else after the user logs in, you'll need a transaction test to evaluate this part of the user experience past the login screen.

Some examples of transaction tests include:

* **Productivity SaaS:** Log in, browse to a shared documents folder, and download a file.
* **Shopping/e-commerce:** Load the main page, search for a specific product by name, add it to a shopping cart, and complete the purchase using a dummy credit card.
* **Web conferencing:** Log in, schedule a meeting, and join the meeting in the browser with a virtual camera and microphone
*   **BrowserBot** is a component of the ThousandEyes

    [Cloud Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/cloud-agents)

    and

    [Enterprise Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents)

    that manages page load and transaction tests. This is accomplished by running an instance of the Chromium web browser which can be driven automatically via Selenium from Node.js. Complete details are available in the

    [What is BrowserBot?](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/what-is-browserbot)

    article.
* **Selenium** is an open source software library for browser automation. Transaction tests leverage the Selenium API in Node.js for automating the Chromium web browser.
* **node-fetch** is an open source software library for making HTTP requests. Transaction tests leverage node-fetch within Node.js for API monitoring, allowing you to script machine-to-machine workflows such as back-end API call sequences.
* **Node.js** is a JavaScript runtime environment included in BrowserBot which is used to execute scripts for transaction tests.
* **JavaScript** is the programming language in which transaction scripts are written. You do not need to be a JavaScript expert to work with transaction tests, but some JavaScript knowledge will allow you to create more advanced transaction scripts.

### Getting Started with the Recorder IDE <a href="#getting-started-with-the-recorder-ide" id="getting-started-with-the-recorder-ide"></a>

The Recorder IDE has two modes, based on your permission settings. Both modes require the `API Access` permission and either the `Login via ThousandEyes login page` or `Login via Single Sign-On` permission.

* **Standalone Mode**: Allows the user to use the IDE for standalone test creation. No additional permissions required.
* **Test Creation Mode**: Allows the user to create tests and export (upload) the tests to the ThousandEyes platform at app.thousandeyes.com. This mode additionally requires the `Edit tests`, `Create web transaction tests`, `View agents in account group`, and `View labels` permissions.

#### Downloading and Installing the Recorder IDE <a href="#downloading-and-installing-the-recorder-ide" id="downloading-and-installing-the-recorder-ide"></a>

Follow the normal installation process for your computer's operating system. For example, the macOS version of the ThousandEyes Recorder downloads as a disk image (.dmg) file. Double-click the downloaded file and a macOS installation dialog opens. In that dialog, drag the application icon into your Applications folder.

After completing the installation, launch the ThousandEyes Recorder IDE. The first time you use the Recorder IDE, you will be prompted to login to your ThousandEyes account. Type your username and password and click the **Log In** button, or click **Single sign-on** if your organization is configured to use an external identity provider for authentication.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1b259339e53d2dc27c08bd59ab10be94bb6d826a%2Fgetting-started-with-transactions-1.png?alt=media)

After completing the login flow, the Recorder IDE may flash briefly while it verifies your user has the necessary permissions. After this, it should look like the screenshot below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fb690d1eab16a4405827ae20b147808fe3f39ac3%2Fgetting-started-with-transactions-2.png?alt=media)

If the Recorder IDE shows the message "You Do Not Have Permissions to Create Tests", as seen below, double check that your ThousandEyes user is assigned a role with the requisite permissions.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-413e24df240dcf0340ebb7b8af27877f4aba811c%2Fgetting-started-with-transactions-3.png?alt=media)

You may also change your current account group by clicking on your e-mail address in the top right corner.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-622695fa65c2f7afa5c2e94da1ec115859eea66c%2Fgetting-started-with-transactions-4.png?alt=media)

### Browser Synthetics Development Workflow <a href="#browser-synthetics-development-workflow" id="browser-synthetics-development-workflow"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6adbd247bd8c422239585ac46b200f889d02f75e%2Fgetting-started-with-transactions-5.png?alt=media)

### Recording a Browser Transaction <a href="#recording-a-browser-transaction" id="recording-a-browser-transaction"></a>

Click the **Record** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5ae7dd1e767f221bd37f7556ae730e71d51a319d%2Frecord-button.png?alt=media)

) and the Recorder IDE will prompt you to type a URL to record. You may also configure the browser window size and orientation. After typing a URL, click **Start Recording** and the Recorder IDE will launch a Chromium browser window which will automatically navigate to that URL.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d658711263790661845bfccafdce3f535f402ed7%2Fgetting-started-with-transactions-6.png?alt=media)

The browser will record your interactions, such as clicking on buttons or typing text in form fields, and use them to automatically generate a transaction script. When you have finished your recording, go back to the Recorder IDE window and click the **Stop** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c341080352abf25296cb43838dd425172f097506%2Fstop-button.png?alt=media)

).

As an example, click the **Record** button and type https://google.com in the **Enter Base URL** field, then click the **Start Recording** button. When the Chromium window has opened and loaded https://google.com, click on the search field, then type "ThousandEyes product documentation", and then press the "Enter" key. On the search results page, click the link to the ThousandEyes product documentation site. Then go back to the Recorder IDE window and click the **Stop** button.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-85a5f724a06a529a375ea1946d9fb7f2460c4c3b%2Fgetting-started-with-transactions-7.gif?alt=media)

After clicking the **Stop** button, the Recorder IDE will close the Chromium window and generate a transaction script for automating the workflow you just recorded. In this example, you should expect to see a script generated like the one below:

import { By, Key } from 'selenium-webdriver';

import { driver, test } from 'thousandeyes';

async function runScript() {

const settings = test.getSettings();

await driver.get(settings.url);

await click(By.name(\`q\`));

await typeText('thousandeyes product documentation', By.name(\`q\`));

await pressEnter(By.name(\`q\`));

// Click on 'ThousandEyes Documentation - Thousa...'

await click(By.css(\`\[href="https://docs.thousandeyes.com/"] > .LC20lb\`));

You have now successfully recorded your first transaction test. The next step in the browser synthetics development workflow is to play the test to verify it works as expected. If you would like a better understanding of the generated code for this transaction script, continue on to the next section below. Otherwise, jump ahead to the

Playback

section.

**Breaking down the script line by line**

The first two lines of the script are import declarations. The transaction script runs in Node.js, a JavaScript runtime environment, and allows us to import code from outside of the script. In this case, the Recorder IDE automatically imported code from two packages named "selenium-webdriver" and "thousandeyes".

import { By, Key } from 'selenium-webdriver';

The first declaration, shown above, imports a class named `By` and an enumeration named `Key` from Selenium. The

[`By`](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index\_exports\_By.html)

class is used for specifying the method for locating an element within a webpage. To interact with an element, like clicking on it or typing into it, Selenium must first be able to locate the element. Elements will be generally located in one of the following ways:

* `className`: Locates elements that have a specific class name.
* `css`: Locates elements using a CSS selector
* `id`: Locates elements by the ID attribute
* `linkText`: Locates link elements whose visible text matches the given string
* `name`: Locates elements whose name attribute has the given value
* `xpath`: Locates elements matching a XPath selector

The

[`Key`](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index\_exports\_Key.html)

enumeration provides representations of pressable keys that aren't text, such as the Alt, Shift, Tab, and Enter keys. The Recorder IDE imported this enumeration because we pressed the Enter key while recording.

import { driver, test } from 'thousandeyes';

The line above calls the `runScript` function, which contains the interactions that were recorded. The `runScript`function is defined in the following lines.

async function runScript() {

This line begins the definition for `runScript` function.

This line calls the `configureDriver` function which is provided by the Recorder IDE. The `configureDriver` function configures the driver instance's implicit timeout. The implicit timeout specifies the maximum amount of time to wait when attempting to locate elements on the page. Without calling `configureDriver`, the default value is 0 which is not very forgiving on modern websites and will often throw errors that elements could not be found because the page had not fully loaded. When `configureDriver` is used, the value is set to 7 seconds.

const settings = test.getSettings();

This line calls the `getSettings` method from the `test` module and stores the result in a variable named `settings`.

await driver.get(settings.url);

This line calls the `get` method of the `driver` instance to navigate to a specific URL. It references the settings variable from the previous line to use the target URL from the test configuration.

await click(By.name(\`q\`));

This line is generated from clicking on the search field on the Google search page. It calls a function named `click`, which is provided by the Recorder IDE, with an element selector using `By.name`, which was imported earlier from Selenium. The value of the name selector, "q", corresponds to the HTML name attribute of the search field on Google’s page.

await typeText('thousandeyes product documentation', By.name(\`q\`));

The `typeText` function is provided by the Recorder IDE as a helper function for typing text into a given field. It accepts two parameters: first, the text to type, and second, a selector to locate the element in which to type that text.

await pressEnter(By.name(\`q\`));

The `pressEnter` function is provided by the Recorder IDE as a helper function for pressing the enter key. It accepts one parameter, a selector to locate the element in which to press the Enter key.

await click(By.css(\`\[href="https://docs.thousandeyes.com/"] > .LC20lb\`));

The last line in the runScript function is generated from clicking on the ThousandEyes Product Documentation link on the search results page. Here, the Recorder IDE used a different selector, `By.css` to locate the link.

The closing curly brace concludes the definition of the `runScript` function.

The helper functions mentioned above that are generated and included by the Recorder IDE, such as `configureDriver`, `click`, `typeText`, and `pressEnter`, are defined below the the definition of the runScript function.

Once you have recorded a transaction, you can play the script to test that it works as expected. Click the **Play** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1b2764b422596a6dda6752bf58433a196b95a67e%2Fplay-button.png?alt=media)

) and the Recorder IDE will launch Chromium to execute the Transaction script.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e4a778bb2c76a34d23d1432a3e3c769990767f31%2Fgetting-started-with-transactions-8.gif?alt=media)

If everything worked correctly, the Chromium window will close and no errors will be reported. If your test playback worked successfully, then you should

optimize

the script by adding markers, screenshots, and configuring credentials, then

export

the script as a scheduled transaction test in the ThousandEyes platform.

If any errors were encountered while executing the script, they will be reported in the Recorder IDE’s console located in the bottom pane of the window, as seen below. When an error occurs, the Recorder IDE will also capture a screenshot from the browser and highlight the lines of code leading to the error. If your test playback encountered errors, then you should proceed to

troubleshooting

the script so that it correctly and completely emulates the user journey without errors.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-13ba2e08a838e2b058d8b199ddf0892e772f13c3%2Fgetting-started-with-transactions-9.png?alt=media)

Once your transaction script successfully plays back without any errors, you should optimize the script with the features described below. After adding your optimizations, be sure to play the transaction again to verify it still works as expected.

You can use markers to define and measure discrete steps within a user journey or business transaction. For example, an e-commerce checkout transaction may include steps for "Item Search", "Add to Cart", and "Submit Order", and each step may include multiple actions like clicking and typing. Markers are used to delineate such steps and measure the time taken for each. By identifying where a script section starts and stops, markers can be compared to over test rounds and to the overall transaction time. If the performance of the whole transaction degrades, markers allow you to quickly see which step(s) in the transaction took longer to complete than they normally would. When an error occurs inside of a marker, the marker will show as "Incomplete" in the test view which can identify the specific phase of the transaction that had an error. Marker times are displayed on the timeline and waterfall in transaction test views and can also be used in alert rules and dashboards.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9156d910f56cef34aef6e79b43a5791bbec3893a%2Fgetting-started-with-transactions-10.png?alt=media)

There are two ways to use markers:

* the `set` method creates a marker with the supplied name that spans from transaction start time to the time this method is called
* the `start` and `stop` methods start and stop a marker with the supplied name at the time they are called

To use markers in your script, you must include the `markers` module in the `thousandeyes` import line at the top of the script.

import { driver, markers, test } from 'thousandeyes';

Clicking the **Add marker** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dd5adc90c2f1a93e0334afcebf82a0b279e22e20%2Fmarkers-button.png?alt=media)

) will:

* Add `markers` to the `import { ... } from 'thousandeyes'` import declaration, if the module is not already imported
* Add two lines of code for `markers.start` and `markers.stop` at the cursor position in the script editor

import { By, Key } from 'selenium-webdriver';

import { driver, markers, test } from 'thousandeyes';

async function runScript() {

const settings = test.getSettings();

await driver.get(settings.url);

// Using markers.set, the ‘Initial Page Load’ marker spans from transaction start time

// to the time the initial page finishes loading

markers.set('Initial Page Load');

// Using markers.start, the ‘Search’ marker begins measuring time after the initial page loaded

await click(By.name(\`q\`));

await typeText('thousandeyes product documentation', By.name(\`q\`));

await pressEnter(By.name(\`q\`));

// Using markers.stop, the \`Search\` marker ends when the user submits the search form

markers.start('Product Docs');

await click(By.css(\`\[href="https://docs.thousandeyes.com/"] > .LC20lb\`));

markers.stop('Product Docs');

Screenshots are useful to track progress and ensure the page visually matches what you were intending to see. You can capture a screenshot of the browser’s viewport by adding the following line of code inside your script. Clicking the **Take screenshot** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-549c266b170be274542ad4ee13b4ab525fd3eb7f%2Fscreenshot-button.png?alt=media)

) will add this line of code at the cursor position in the script editor. No additional import declarations are required because the takeScreenshot method belongs to the driver class that has already been imported after the recording.

await driver.takeScreenshot();

There is no limit to the number of screenshots that can be captured during a transaction, but only the last three screenshots will be included with the test results in the platform. It can still be useful to capture more than three screenshots because if the script encounters an error before completing, you can inspect the state of the webpage leading up to the error. One screenshot will be automatically captured at the time the error occurs.

Capturing screenshots requires a small-but-non-zero amount of time on the order of one half second. Whenever possible screenshots should not be captured gratuitously and should be captured after stopping one marker and before starting the next.

You can disable screenshots by unchecking the **Screenshots > Enabled** checkbox in the test's **Advanced Settings** tab in the ThousandEyes platform. Unchecking this box will prevent screenshots from being captured when `driver.takeScreenshot()` is called or when an error occurs.

The Recorder IDE’s Chromium browser will record the keys you press while interacting with a page. Recall from the example Google search transaction that typing in the search form resulted in this line in the transaction script:

await typeText('thousandeyes product documentation', By.name(\`q\`));

In some cases, such as typing in password forms, you may not want to store the values you typed as cleartext in the transaction script. ThousandEyes provides a credential repository which is used to store and retrieve sensitive information like passwords, authentication tokens, or two-factor authentication secrets.

The Recorder IDE will automatically use the credentials repository if you record typing in an input field with a type attribute equal to "password". As an example, start a new recording on the URL https://app.thousandeyes.com and when the Chromium window opens and loads the ThousandEyes login page, click on the **Password** input field and type some text, and then click the **Log In** button. Switch back to the Recorder IDE window, click the **Stop** button.

Notice how the call to the `typeText` function differs from the earlier example:

await typeText(credentials.get('pass\_1674485288249'), By.id(\`password\`));

The Recorder IDE detected we were typing in a "password" field and automatically stored the value as a local credential rather than using a plaintext string. Instead of seeing the characters you typed, the first parameter of the `typeText` function is now a call to `credentials.get` with a credential name of "pass\_1674485288249". The credential name is generated using the current unix timestamp to avoid naming collisions with other credentials. While you can use the credential with its default name, the recommended best practice is to update the credential name to something meaningful or identifiable.

Credentials can be managed in the Recorder IDE’s credentials dialog by clicking the **Show credentials** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6b7ede05af1fbbff57acece994e6a6f48aa43e43%2Fcreds-button.png?alt=media)

). This dialog contains two sections: the credential repository from the ThousandEyes platform and local credentials (those that have not yet been synced to the ThousandEyes platform). To rename a credential, hover over the credential name in the list, then click the pencil icon. Then, you can edit both the name and the value of the credential. Click the **Update Credential** button to save your changes.

| Credentials List                                                                                                                                                                                                                                                                              | Credential Details                                                                                                                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>​</p><p><img src="https://2360053865-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4aa9185cf516a04e4e99a8a4fddbd755b1708ea0%2Fgetting-started-with-transactions-11.png?alt=media" alt="" data-size="original"></p><p>​</p> | <p>​</p><p><img src="https://2360053865-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bda49e0d2b7c2349f7b97fcac525cdee1e68b238%2Fgetting-started-with-transactions-12.png?alt=media" alt="" data-size="original"></p><p>​</p> |

After you rename a credential, be sure to modify the name in any calls to credentials.get that used the old name. For example, if you rename the "pass\_1674485288249" credential to "myPassword", then you must update the `typeText` line from above like so:

await typeText(credentials.get('myPassword'), By.id(\`password\`));

You can also sync the credential to the ThousandEyes platform by hovering over the credential name in the list and clicking the **Save to ThousandEyes** icon. If you plan to export this transaction to the platform, you should sync your credential now.

You may find that some recorded transactions will raise an unexpected error during playback in the Recorder IDE or while running on Cloud and Enterprise Agents in the ThousandEyes platform. While many recorded flows will result in fully functional scripts that work on the first playback, at times it will be necessary to manually alter the recorded output. This section will help you to troubleshoot your transaction scripts to identify the cause of errors and how to fix them.

To most effectively troubleshoot transaction scripts, you should have some familiarity with the browser's web development tools. See the

[Working With Web Development Tools](https://docs.thousandeyes.com/product-documentation/browser-synthetics/transaction-tests/getting-started/working-with-web-development-tools)

article for more information and resources.

#### Useful Functions for Troubleshooting <a href="#useful-functions-for-troubleshooting" id="useful-functions-for-troubleshooting"></a>

You can use `console.log` statements to help debug, such as printing the current line number, e.g. `console.log("Line 7")`, or the value of a variable, e.g, `console.log(settings.url)`.

You can use `driver.sleep` to slow down script execution when debugging or if you want to sit at one step for a long time (for instance, to inspect elements in the page using the web development tools). The `driver.sleep` function takes a single parameter, the amount of time to sleep in milliseconds. Example usage:

await driver.sleep(5 \* 1000);

Clicking the **Add sleep** button (

![](https://github.com/thousandeyes/docs/blob/prod/.gitbook/assets/getting-started/getting-started-with-transactions/sleep-button.png)

) will insert code to call `driver.sleep` at the cursor position in the script editor.

The most common error is `NoSuchElementError` which indicates that Selenium was unable to locate an element within the page with the given selector. This usually occurs for one of the reasons explained below.

**Element did not exist (yet)**

Today's web applications commonly use client-side rendering to build their pages. Compared to server-side rendering, which generates the full HTML document and sends it to the client in the initial request, with client-side rendering the server only sends an initial scaffold in the first request and then uses JavaScript to dynamically fetch data and render it in the page. Selenium will begin its attempt to locate an element after the initial page load, but does not necessarily wait for all the JavaScript to finish executing.

If the transaction is failing because it cannot locate an element, you can try increasing the `implicit` value in the `configureDriver` function. For example, the code below sets the implicit wait to 15 seconds, a little more than double the Recorder IDE's default value. Note that the value is in milliseconds, which is why `* 1000` is used.

async function configureDriver() {

await driver.manage().setTimeouts({

implicit: 15 \* 1000, // If an element is not found, reattempt for this many milliseconds

**Element did exist, but selector did not match**

Some pages contain elements that do not have consistent attributes which may cause the Recorder IDE to choose a selector that matches while recording but does not match during playback. There are two easy ways to identify if this is the cause of your `NoSuchElementError`:

1.  1\.

    Use the `console.log` and `driver.sleep` functions immediately before the line of code which raises the `NoSuchElementError` and play the transaction again. After the browser opens, switch back to the Recorder IDE and when you see your log message in the Recorder IDE's console, hit the **Pause** button. Return to the browser and use the web development tools to inspect the element, comparing its attributes with the selector used in the script. It may be helpful to repeat this more than once.
2.  2\.

    Re-record your transaction and compare the selector(s) between the first and second recordings. Make sure to copy or save the original recording before starting a new one because the new recording will overwrite the original script in the script editor.

**Element was in a different tab or window**

Some browser actions may cause a new browser tab (or window) to open. While the Recorder IDE will continue to record your actions in other tabs, it does not record when you switch between them. This can lead to the script looking for an element in one page when it exists in another page in a different tab.

1.  1\.

    ​

    [`switchToNextTab.js`](https://github.com/thousandeyes/transaction-scripting-examples/blob/master/examples/switchToNextTab.js)

    : Shows how to switch to the next tab, including wrapping around to the first tab from the last tab

**ElementClickInterceptedError**

The `ElementClickInterceptedError` will occur when Selenium attempts to click on an element but it is covered by one or more other elements. This can happen when the web page uses the CSS `z-index` property to overlay elements on top of other elements. This normally occurs when a popup dialog is shown or when sticky navigation bars or footers scroll with the page.

To avoid this error, be sure to wait for and dismiss any automatic modal popups while recording. If the target element is covered by a sticky navbar or footer, try using the

[`scrollElementIntoView`](https://github.com/thousandeyes/transaction-scripting-examples/blob/master/examples/scrollElementIntoView.js)

function from the from the transaction scripting examples repository.

**ElementNotInteractableError and WebDriverError: element not interactable**

These errors will occur when Selenium attempts to interact (e.g, click on or type into) with an element that is not visible. In contrast to the `NoSuchElementError`, the element does exist and was successfully located, but Selenium cannot interact with it because it is not rendered in the page.

This commonly occurs when interacting with an element that is only visible while hovering the mouse pointer over a particular part of the page. The Recorder IDE does not record mouse hover events, so you will need to add the code to move the mouse pointer. There are two ways you may be able to resolve this issue:

1.  1\.

    Re-record the transaction and try clicking the element, not just hovering over it. Many pages will handle clicks and hovers the the same way, though some may handle them differently.
2.  2\.

    Use the `moveMouseInto` function from

    [`moveMouseIntoElement.js`](https://github.com/thousandeyes/transaction-scripting-examples/blob/master/examples/moveMouseIntoElement.js)

    in the transaction scripting examples repository to move the mouse pointer to a specific element and trigger hover events.

**TimeoutError: Transaction timed out**

This error occurs when the configured test timeout is reached before the script has completed. To prevent this error, you can increase the test timeout or reduce the runtime of the script. For example, you can make the script run faster by minimizing or removing use of `driver.sleep`. If your transaction is lengthy or complex with lots of steps, consider breaking it down into two or more separate transactions.

The maximum configurable timeout is dependent on the test interval:

* 60 seconds for 2 minute tests
* 150 seconds for 5 minute tests
* 180 seconds for 10+ minute tests

To configure the timeout in the Recorder IDE, click the **Show settings** button (

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3df9621efbce4cf0c5a2ce5c2e764adf7a9239c2%2Fsettings-button.png?alt=media)

) and adjust the **Timeout** slider in the **Advanced Settings** tab. To configure the timeout in the ThousandEyes platform, go to the **Test Settings** page, find and expand the test in the list, and adjust the **Timeout** slider in **Transaction Timing** section of the **Advanced Settings** tab.

### Export to ThousandEyes Platform <a href="#export-to-thousandeyes-platform" id="export-to-thousandeyes-platform"></a>

After you've recorded, optimized, and played back your transaction, you are ready to export it from the Recorder IDE to the ThousandEyes platform. Click the **Export to ThousandEyes** button to open the **Test Settings** dialog where you can select the test interval and agents, associate alert rules, and configure other advanced settings.

| Basic Settings                                                                                                                                                                                                                                                                      | Browser Options                                                                                                                                                                                                                                                                 | Advanced Settings                                                                                                                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>​</p><p><img src="https://2360053865-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-581cc3967131958c0790c8c150a2af69aec0cf98%2Fexport-basic-configuration.png?alt=media" alt="" data-size="original"></p><p>​</p> | <p>​</p><p><img src="https://2360053865-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b2184b1bc6257b20a4026d6fc98ad6ea8b5af08a%2Fexport-browser-options.png?alt=media" alt="" data-size="original"></p><p>​</p> | <p>​</p><p><img src="https://2360053865-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a65bbdea2cc3a142a9a63ecfda6d17872053a12a%2Fexport-advanced-settings.png?alt=media" alt="" data-size="original"></p><p>​</p> |

As mentioned in the \[Requirements]\(#requirements) section above, exporting to the ThousandEyes platform requires the necessary permissions to use the Recorder IDE in Test Creation Mode. If you are using the Recorder IDE in Standalone Mode, you can save your transaction script locally to share it with your ThousandEyes administrator. Click the \*\*More actions\*\* button (!\[]\(/.gitbook/assets/getting-started/getting-started-with-transactions/more-actions-button.png)), then click the \*\*Save Script\*\* menu item.

When you are finished configuring the settings, click the **Export** button and the Recorder IDE will create a new test in the ThousandEyes platform. When it's finished, you should see a confirmation dialog indicating the test was successfully saved. Click the **View test** link in this dialog to open the test settings in platform and validate the test.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f7ff391e388a4e5ed5a2225eaaae543dabd637cb%2Fexport-view-test.png?alt=media)

If you are using the Recorder IDE in Test Creation Mode and your script uses any credentials which have not been synced to the ThousandEyes platform, you will receive a confirmation dialog to create the test. You can either click the **Cancel** button and sync the credentials before creating the test, or you can click **Create Test** and then sync the credentials afterwards.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-946754da077315173ab38903484ff970b4d10b32%2Fexport-credentials-warning.png?alt=media)

It is important to validate that the transaction runs successfully on the agents in the platform even though you have already played back the transaction locally in the Recorder IDE. The Recorder IDE is very closely related to the BrowserBot that runs inside the ThousandEyes Cloud or Enterprise Agent, but the they are not identical. This means that in some transactions, a script which successfully played back in the Recorder IDE may fail when run from agents in the platform.

After you export your test, click the **View test** link in the success dialog to open the test settings in platform. At the bottom of the test settings panel, click the **Run Once** button to run an instant test in a new browser tab. Wait for the test results and then verify that all of the agents successfully completed the transaction. If any errors occur, click the **Run Again** link above the timeline in the view to determine if the error is consistent or intermittent. Then, refer back to the

troubleshooting

section to determine the cause of the error.

**My script works in the recorder, but fails in the platform. Why?**

**User Agent**: The default curl user agent we use for HTTP tests is rejected by many larger sites. You should supply a chrome user agent or similar so that all layers use the same UA. You can configure the user agent in the **HTTP Request** section of the **Advanced Settings** tab in the test's settings.

**Agent Location**: Scripts that work fine locally may fail on agents in other regions, as they may be routed differently, land on different sites etc. Make sure you rule out any location specific issues.

**Agent Network Conditions**: The time that network requests take can have an impact on whether your script works or not. For example, if you have a driver.sleep command that waits for 5 seconds, that may work for you but not be sufficient for an agent in some far off rural area. It's best to not use hard coded sleep values, but instead use waits with sufficient timeouts.

**Authentication**: If you test an application that uses Integrated Windows Authentication (IWA), it may behave differently while recording in Windows than it does while running on the Linux-based cloud and enterprise agents. IWA, sometimes called "silent authentication", uses your Windows credentials to automatically authenticate to a web server without an interactive login form, resulting in a different transaction workflow from a Windows device than a cloud or enterprise agent. IWA is commonly used for internal applications or intranet sites, but may also be used with SaaS applications when they are configured with federated single sign-on.

**Network Security**: When the transaction runs on the agent, it is almost always from a different network than where it was originally recorded. This can cause different firewall or proxy rules to apply and block the traffic coming from the agent. If the transaction test completes during playback in the Recorder IDE but fails in the ThousandEyes platform, you should check the network layer metrics and path visualization to ensure the agent is able to reach the target. For Enterprise Agents, you may need to

[configure a proxy](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/proxy/configuring-an-enterprise-agent-to-use-a-proxy-server)

or verify that the

[necessary fire rules](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/configuring/firewall-configuration-for-enterprise-agents)

are in place.

### Using the Transaction Test View <a href="#using-the-transaction-test-view" id="using-the-transaction-test-view"></a>

When you export a Transaction test, you can see the test data under **Cloud & Enterprise Agents > Views**. The Transaction view leverages the ThousandEyes standard layout,

[documented here](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/viewing-data#thousandeyes-standard-layout)

. For general information on the ThousandEyes standard view layout, see

[Getting Started with Views](https://docs.thousandeyes.com/product-documentation/getting-started/getting-started-with-views)

. This section highlights specifics shown in the Transaction view.

#### Transaction View, Timeline <a href="#transaction-view-timeline" id="transaction-view-timeline"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f5d7edce23ebda0d783369efdffdabb39242577a%2Ftx-view-timeline.png?alt=media)

The top of the Transaction view shows a timeline similar to other views, with a time period slider below. Three metrics can be displayed on the timeline:

* **Transaction Time (default):** The amount of time spent running the transaction test. When Transaction Time is selected, you may also select up to three markers to view on the timeline
* **Errors:** The number of timeout errors, page errors, assert errors, and other errors that occurred in the test round
* **Completion:** Whether or not the transaction completed without errors

When a single agent is selected, you can mouse over the error indicator in the swimlane under the timeline to view the specific error details.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-28092d112e9ae2ad4ba5a58059013d0a73d89fc6%2Ftx-view-map-all.png?alt=media)

The **Map** tab as shown below displays a global map showing all of the agents that are running the test, with a **Metrics** panel to summarize data and any error messages reported by the agents. Clicking on an agent in the map will select that agent in the **Agent** selector above the timeline. The color of the agents shown on the map indicates the speed relative to the test duration, as specified by the **Timeout** parameter in the **Advanced Settings** tab for the test configuration in **Cloud & Enterprise Agents > Test Settings**.

The **Metrics** panel shows the transaction time (average, when all agents are selected) and when a single agent is selected also shows the individual marker times.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ed54f069ffa4128e749da2ab57693c48fc0aa6df%2Ftx-view-map-single.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cf580f711c21f307a63ef6aaa2739106f77b40bb%2Ftx-view-table.png?alt=media)

The **Table** tab shows test details from the selected test round for each agent. If any errors occur during the transaction, the agent will be shown in the table with a red dot next to its name. You can mouse over this icon to view specific error details. Clicking on an agent in the table will select that agent in the **Agent** selector above the timeline.

#### Transaction View, Waterfall <a href="#transaction-view-waterfall" id="transaction-view-waterfall"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7817406e655a9e458d310035f36440fd1297cb0e%2Ftx-view-waterfall.png?alt=media)

The **Waterfall** tab in the transaction view is similar to the **Waterfall** tab in the page load view, with three additional features at the top of the chart:

* **Pages**: Because transaction tests can navigate through more than one page, the waterfall chart in the transactions view indicates each page that is visited and the duration of time spent on that page. You can mouse over a page in the **Page** row to view the page's duration. You can click on a page to filter the waterfall chart to only include components from that page.
* **Markers**: Markers are exclusive to transaction tests. The waterfall chart for transactions includes a visualization of the marker timings over the duration of the transaction. You can mouse over a marker in the **Markers** row to view the marker's exact timing. You can click a marker to filter the waterfall chart to only include components during that marker.
* **Screenshots**: The last three screenshots captured during the transaction will be stored with the test data and displayed on the **Waterfall** tab. You can mouse over the picture icon in the **Screenshots** row to view the captured screenshot. The horizontal position of the icon in the row indicates the relative point in time during the transaction that the screenshot was captured.

#### ThousandEyes Product Documentation <a href="#thousandeyes-product-documentation" id="thousandeyes-product-documentation"></a>
