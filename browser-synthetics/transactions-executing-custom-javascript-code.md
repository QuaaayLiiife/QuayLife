# Transactions – Executing Custom JavaScript Code

The flow of a ThousandEyes transaction test is defined with JavaScript code. Similarly, frontends of modern web applications are also implemented using JavaScript code. The evident similarity intuitively can lead to an incorrect conclusion that execution contexts of transaction test control code and of tested web application are somehow interlinked, which is not exactly the case.

This article briefly discusses differences between two main JavaScript code execution contexts and provides instructions on how to implement a transaction that executes custom JavaScript code in the context of the tested web application. See

[Upgrading to BrowserBot 2.6+ (Chromium 97)](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/upgrading-to-browserbot-26)

for more information on recent BrowserBot upgrades that might impact your existing transaction scripts.

### BrowserBot Versus Chromium Web Browser <a href="#browserbot-versus-chromium-web-browser" id="browserbot-versus-chromium-web-browser"></a>

ThousandEyes Cloud and Enterprise Agents utilize the

[BrowserBot](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/what-is-browserbot)

component for running transaction (and page load) tests. To be precise, the BrowserBot component actually consists of two parts:

* The **BrowserBot** itself is the control center of the transaction test execution - when the agent requires a transaction test to be executed, the task is dispatched to BrowserBot. The BrowserBot, upon receiving a new transaction test execution task, runs the received task and controls the browser as specified by the transaction test code. You could think of BrowserBot as a human, sitting behind a computer on which a web browser is running, using that browser to navigate web applications as instructed by a transaction script.
* **Chromium web browser** is the web browser that the BrowserBot is "driving around" by performing transaction steps such as mouse clicks, keyboard inputs, waiting conditions, etc.

To summarize, BrowserBot and Chromium web browser (and a few other bits) are separate pieces of software that constitute the entire BrowserBot component. These pieces of software talk to each other through a set of well-defined interfaces and should not, at least for the purpose of this discussion, be thought of as one monolithic application.

### Transaction Control Execution Context <a href="#transaction-control-execution-context" id="transaction-control-execution-context"></a>

A ThousandEyes transaction test is defined using JavaScript code. Here is an example of a very simple transaction test implementation:

import { driver } from 'thousandeyes';

async function runScript() {

await driver.get('https://google.com');

await driver.takeScreenshot();

This transaction does the following:

This code runs in what we call a _transaction control execution context_ - an isolated,

[Node.js](https://nodejs.org/)

\-powered environment. To simplify, one can imagine that transaction code runs inside the BrowserBot and tells the BrowserBot how to interact with the Chromium web browser. The available methods of interaction with the web browser are described in detail in the

[Transaction Scripting Reference](broken-reference)

.

### Web Application (Browser) Execution Context <a href="#web-application-browser-execution-context" id="web-application-browser-execution-context"></a>

This execution context takes place in a web browser. One of the simpler ways to explain this execution context is by showing an equivalent way of executing custom JavaScript code inside the web application context - by using the **Console** tab of the

[Chrome/Chromium browser developer tools](https://developers.google.com/web/tools/chrome-devtools/)

.

Using your web browser, navigate to the target web application (in our case

[https://google.com](https://google.com/)

) and open the browser developer tools. Switch to the **Console** tab and enter the custom code to be executed in the application context.

Here is an example of using custom code to trigger an alert dialog:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-94b5e07208f4af5d986325db5801083af06aafec%2Fproduct-documentation\_tests\_transactions-executing-custom-javascript-code-1.png?alt=media)

### Executing Custom JavaScript in a Target Web Application <a href="#executing-custom-javascript-in-a-target-web-application" id="executing-custom-javascript-in-a-target-web-application"></a>

Let's suppose that we want to add a big block of text to the application that we are testing. Here is a sample JavaScript code that enables us to achieve that:

var h = document.createElement("h1");

var t = document.createTextNode("ADDING THIS TEXT ELEMENT TO THE PAGE, JUST FOR FUN");

document.body.appendChild(h);

While you can quickly test the above code in your browser developer tools, this code cannot simply be added to the transaction test control code, as transaction control execution context has no `document` reference available.

Instead, the `executeScript()` method of the `driver` object of the `thousandeyes` module enables passing custom JavaScript code into the web application (browser) context and executing it there:

import { driver } from 'thousandeyes';

async function runScript() {

await driver.get('https://google.com');

await driver.executeScript(

'var h = document.createElement("h1"); ' +

'var t = document.createTextNode("ADD THIS \<h1> TEXT ELEMENT TO THE PAGE, JUST FOR FUN"); ' +

'document.body.appendChild(h);'

await driver.takeScreenshot();

It is important to note that the custom code to be executed in the web browser context is passed to the `executeScript()` method **as a string** (regular text).

The added code above results in the following transaction screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-964858ee1d744d94acbf4d20ef4ce51f8268e46b%2Fproduct-documentation\_tests\_transactions-executing-custom-javascript-code-2.png?alt=media)
