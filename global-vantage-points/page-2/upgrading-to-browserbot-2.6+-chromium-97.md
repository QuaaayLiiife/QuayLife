# Upgrading to BrowserBot 2.6+ (Chromium 97)

Building on the

[BrowserBot 2 upgrade](broken-reference)

, BrowserBot 2.6.0+ provides an upgrade to the Chrome browser used in the Enterprise and Cloud Agent to run page load and transaction tests. This upgrade improves IDE stability for macOS devices and enables additional features in browser-based tests from Chrome.

Between Chromium v80 (prior to BrowserBot 2.6.0) and Chromium v97 (BrowserBot 2.6.0 and after), we've identified a handful of cases where the scripting syntax has changed between these Chromium versions.

#### Issue: After an iframe is destroyed, Selenium Webdriver doesn't automatically switch to the default content <a href="#issue-after-an-iframe-is-destroyed-selenium-webdriver-doesnt-automatically-switch-to-the-default-con" id="issue-after-an-iframe-is-destroyed-selenium-webdriver-doesnt-automatically-switch-to-the-default-con"></a>

Starting with Chromium v80, when iframes are destroyed, Chromedriver doesn't change context to the default content or parent frame. Script creators should explicitly switch to the default content or parent frame after the iframe has been destroyed.

* The script contains either `await driver.switchTo().frame()` or `await driver.wait(until.ableToSwitchToFrame())`.
* The test times out after some action, usually after clicking a submit button; or some element cannot be found even though the screenshot tells us that the element is there and the waterfall looks normal.
* The script throws either `WebDriverError: unknown error: Runtime.evaluate threw exception: TypeError: Cannot read properties of null (reading 'cdc_adoQpoasnfa76pfcZLmcfl_Promise')` or `NoSuchWindowError: no such window`. These errors are thrown when an action is attempted within the context of an iframe that has been destroyed.

In the case of `WebDriverError` or `NoSuchWindowError` errors, the stack trace can tell you which command is failing. The fix is to switch to the default content before the failing command:

await driver.switchTo().defaultContent();

await driver.switchTo().frame()

await driver.switchTo().defaultContent();

await driver.wait(until.ableToSwitchToFrame())

In other cases, where the errors are processed by the script or where the command simply times out, debug the script using markers, identify which command is failing, and switch to the default content before that failing command.

#### Issue: HTML elements with an area of zero are no longer clickable <a href="#issue-html-elements-with-an-area-of-zero-are-no-longer-clickable" id="issue-html-elements-with-an-area-of-zero-are-no-longer-clickable"></a>

Starting with version 83, Chromedriver doesn't click on an element that is outside of the viewport or that has a size of zero in one of its dimensions.

* The script throws `o: element not interactable: element has zero size`.
* The script is attempting to scroll to the element, but the element is still not visible in the viewport.

Verify that the element is in the viewport by scrolling up or down to the element:

const element = await driver.findElement(...

const scrollIntoViewOptions = { block: 'center' };

await driver.executeScript(

\`arguments\[0].scrollIntoView(arguments\[1]);\`,

element, scrollIntoViewOptions);

If the element is already in the viewport, it could be that the effective size of the element is zero. In this case an easy solution is to click the element via Javascript:

const element = await driver.findElement(...

await driver.executeScript(\`arguments\[0].click();\`,element);

It is always a good practice to inspect the HTML element, verify that the element's area is not zero, and change the selector accordingly.

#### Issue: shadowRoot no longer returns a WebElement <a href="#issue-shadowroot-no-longer-returns-a-webelement" id="issue-shadowroot-no-longer-returns-a-webelement"></a>

Starting with version 96, Chromedriver has made its shadowRoot values compliant with the updated W3C WebDriver specification. This means that calling this property of WebElement won’t return another WebElement, but returns a shadowRoot reference. For more information, see

[the W3C specification](https://w3c.github.io/webdriver/#get-element-shadow-root)

.

Fortunately, Selenium Webdriver offers a new API endpoint to access to these elements and locate elements within a shadow root.

* The script contains `const shadowRoot = await driver.executeScript(`\``return arguments[0].shadowRoot;`\``, element);`.
* The script fails with `TypeError: shadowRoot.findElement is not a function` or similar when performing an action on the shadow root.

For sake of simplicity and portability, replace the JavaScript code with the new API endpoint call to get the shadow root:

const element = await driver.findElement(...);

// Get the shadow root as an instance of ShadowRoot

const shadowRoot = await element.getShadowRoot();

// Find more elements within the shadow root.

const nestedElement = await shadowRoot.findElement(...);

// Now you can handle these elements as regular WebElements

You can still use the shadow root that the JavaScript code returns, but you’ll need to resolve the promise of the `findElement` method before attempting an action on it. This is because of `shadowRoot.findElement`. For example:

let shadowRoot = await driver.executeScript(\`return arguments\[0].shadowRoot;\`, element);

// Selenium allows to call click immediately on the

// promise. Note that this promise hasn't been resolved.

.findElement(By.css('.my-class'))

let shadowRoot = await driver.executeScript(\`return arguments\[0].shadowRoot;\`, element);

// Note that the findElement action is now enclosed

// within parentheses. This way, we resolve the promise

// of the WebElement first & then click on the element.

( await shadowRoot.findElement(By.css('.my-class')) )

#### Issue: Chromedriver does not wait for the HTML document to be loaded completely <a href="#issue-chromedriver-does-not-wait-for-the-html-document-to-be-loaded-completely" id="issue-chromedriver-does-not-wait-for-the-html-document-to-be-loaded-completely"></a>

Some webpages add their scripts at the end of the HTML body, and let the HTML elements load before the JavaScript code is processed by the browser engine.

HTML is loaded and executed line by line. So when the browser encounters a `<script>` tag, it loads and executes the JavaScript code on the spot. For example:

\<button type="button" onclick="doLogin();" >

\<script type="text/javascript">

In this case, the `button` element is loaded and is interactable before the JavaScript function `doLogin` is ready to be executed.

Chromedriver doesn't wait for the document to be completely loaded; the script can start interacting with elements even if all the document hasn't been loaded. In these cases, the JavaScript code is not ready.

* Error occurs almost at the beginning of a new page navigation.
*   The error occurs after an interaction with a WebElement that seems to work fine but does not trigger any action:

    await driver.get('https://url.com/');

    const button = await driver.findElement(...);

    \* This click should trigger some request, redirection

    \* or change in the webpage

    \* Button click does not throw any error

    \* but, by taking an screenshot or inspecting the watefall,

    \* it doesn't trigger any action on the wabpage

    await driver.takeScreenshot();

    \* Script fails because the click was supposed

    \* to be successful & this new element should be present

    const input = await driver.findElement(...);

    await input.sendKeys(...);
*   The WebElement that didn’t trigger any action calls a global JavaScript function from one of its event attributes:

    \<button type="button" onclick="doLogin()" >
*   The sandbox logs shows that some JavaScript functions are not defined:

    \#################### chrome ####################

    \[0902/030003.061733:INFO:CONSOLE(106)] "Uncaught ReferenceError: doLogin is not defined",

Use `document.readyState` to track the state of the document. All of the JavaScript code should be loaded when the value of `document.readyState` is complete. You can add an explicit wait to handle this:

async function runScript() {

// A new page is navigated

// Wait for document ready

// WebElement that didn't trigger any action

await driver.findElement(...).click();

async function waitForReady() {

await simulateHumanDelay();

const configuredTimeouts = await driver.manage().getTimeouts();

const clickAttemptEndTime = Date.now() + configuredTimeouts.implicit;

await reattemptUntil(documentIsReady, clickAttemptEndTime);

async function documentIsReady() {

const state = await driver.executeScript('return document.readyState');

if (state !== 'complete') {

throw Error('Document not ready');

async function reattemptUntil(attemptActionFn, attemptEndTime) {

const TIME\_BETWEEN\_ATTEMPTS = 100;

let numberOfAttempts = 0;

while (Date.now() < attemptEndTime || numberOfAttempts === 0) {

await driver.sleep(TIME\_BETWEEN\_ATTEMPTS);

continue; // Attempt failed, reattempt

break; // Attempt succeeded, stop attempting

const wasAttemptSuccessful = !attemptError;

if (!wasAttemptSuccessful) {

async function simulateHumanDelay() {
