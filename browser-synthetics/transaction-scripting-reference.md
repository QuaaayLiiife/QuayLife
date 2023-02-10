# Transaction Scripting Reference

This article contains a reference of all namespaces, classes, modules and methods that are available for creating

[transaction tests](broken-reference)

.

For Selenium WebDriver documentation, visit

[this page](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/)

​

Hover over a keyword or method name in a script to see additional information, in both the ThousandEyes Recorder and the ThousandEyes platform on the test creation page.

### Getting Test Configuration Settings <a href="#getting-test-configuration-settings" id="getting-test-configuration-settings"></a>

Use `test` to work with the ThousandEyes transaction test configuration, such as getting the target test URL (for example https://google.com/) or getting the test timeout setting.

| **Namespace**     | `thousandeyes`                                                                                                        |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Module**        | `test`                                                                                                                |
| **Import Syntax** | `import { test } from 'thousandeyes'`                                                                                 |
| **Used Like**     | `const settings = test.getSettings();`                                                                                |
| **Method**        | `getSettings()`                                                                                                       |
| **Description**   | Returns an object with the current settings of the test.                                                              |
| **Parameters**    | None                                                                                                                  |
| **Returns**       | (object) with the following parameters: `interval` (number), `timeout` (number), `url` (string) and `proxy` (object). |

#### Sample Script 1: Obtain Test URL <a href="#sample-script-1-obtain-test-url" id="sample-script-1-obtain-test-url"></a>

import { By, Key, until } from 'selenium-webdriver';

import { driver, markers, credentials, downloads, transaction, authentication, test } from 'thousandeyes';

async function runScript() {

const settings = test.getSettings();

await driver.get(settings.url);

await driver.takeScreenshot();

markers.start('SearchForWebdriver');

await driver.findElement(By.name('q')).sendKeys('webdriver', Key.RETURN);

await driver.takeScreenshot();

markers.stop('SearchForWebdriver');

// Wait for full page load

await driver.wait(until.titleIs('webdriver - Google Search'), 1000);

await driver.takeScreenshot();

#### Sample Script 2: Reduce Test Timeout Value <a href="#sample-script-2-reduce-test-timeout-value" id="sample-script-2-reduce-test-timeout-value"></a>

This snippet shows how to get the test timeout setting and set the implicit timeout in the transaction to half that value. On the ThousandEyes platform, this test timeout setting is found on the **Advanced Settings** tab for the transaction test you’re working with, on the **Cloud & Enterprise Agents > Test Settings** screen.

Why would you want to do this? The implicit timeout is the time that each transaction step will wait for a designated page element to appear before timing out. By default, the ThousandEyes Recorder sets the implicit step timeout value to 7 seconds. This per-step value may need to be increased for tests that take longer to complete.

Instead of statically increasing the implicit timeout value in the script, you can configure it to be a proportion (for example 50%) of the total test timeout value. This will ensure the implicit timeout value is always set to a reasonable value, regardless of the test timeout setting.

import { By, Key } from 'selenium-webdriver';

import { driver, test } from 'thousandeyes';

async function runScript() {

const settings = test.getSettings();

await driver.get(settings.url);

async function configureDriver() {

const settings = test.getSettings()

await driver.manage().setTimeouts({

implicit: settings.timeout/2 \* 1000

ThousandEyes provides a wrapper of the Selenium WebDriver library for JavaScript. It contains methods for controlling the browser that is used to execute the test.

| **Namespace**         | `thousandeyes`                                                                                             |
| --------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Module**            | `driver`                                                                                                   |
| **Import Syntax**     | `import { driver } from 'thousandeyes';`                                                                   |
| **Used Like**         | `await driver.get('https://google.com');`                                                                  |
| **Supported methods** | `await driver.get('https://google.com');`                                                                  |
| ​                     | `actions( options )`                                                                                       |
| ​                     | `executeAsyncScript( script, ...args )`                                                                    |
| ​                     | `executeScript( script, ...args )`                                                                         |
| ​                     | `findElement( locator )`                                                                                   |
| ​                     | `findElements( locator )`                                                                                  |
| ​                     | `get( url )`                                                                                               |
| ​                     | `getAllWindowHandles()`                                                                                    |
| ​                     | `getCurrentUrl()`                                                                                          |
| ​                     | `getPageSource()`                                                                                          |
| ​                     | `getTitle()`                                                                                               |
| ​                     | `getWindowHandle()`                                                                                        |
| ​                     | `manage()`                                                                                                 |
| ​                     | `navigate()`                                                                                               |
| ​                     | `sleep( ms )`                                                                                              |
| ​                     | `switchTo()`                                                                                               |
| ​                     | `wait( condition, timeout, message )`                                                                      |
| **Reference**         | https://selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index\_exports\_WebDriver.html |

### Interacting with Page Elements <a href="#interacting-with-page-elements" id="interacting-with-page-elements"></a>

A set of methods for interacting with elements. Once the element is located and retrieved (by using the `findElement()` function or similar), it can be managed using the following methods.

| **Namespace**         | `selenium-webdriver`                                                                                        |
| --------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Module**            | `WebElement`                                                                                                |
| **Find an element**   | `const element = await driver.findElement(By.css('.someClass'))`                                            |
| **Supported methods** | `clear()`                                                                                                   |
| ​                     | `click()`                                                                                                   |
| ​                     | `getAttribute( attributeName )`                                                                             |
| ​                     | `getCssValue( cssStyleProperty )`                                                                           |
| ​                     | `getId()`                                                                                                   |
| ​                     | `getText()`                                                                                                 |
| ​                     | `sendKeys( ...args )`                                                                                       |
| ​                     | `submit()`                                                                                                  |
| **Reference**         | https://selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index\_exports\_WebElement.html |

Defines common conditions for use with WebDriver wait.

| **Namespace**         | `selenium-webdriver`                                                                               |
| --------------------- | -------------------------------------------------------------------------------------------------- |
| **Module**            | `until`                                                                                            |
| **Import Syntax**     | `import { until } from 'selenium-webdriver';`                                                      |
| **Used Like**         | `await driver.wait(until.alertIsPresent(), 10 * 1000, 'Alert did not appear within 10 seconds!');` |
| **Supported methods** | `ableToSwitchToFrame( frame )`                                                                     |
| ​                     | `alertIsPresent()`                                                                                 |
| ​                     | `elementIsDisabled( element )`                                                                     |
| ​                     | `elementIsEnabled( element )`                                                                      |
| ​                     | `elementIsNotSelected( element )`                                                                  |
| ​                     | `elementIsNotVisible( element )`                                                                   |
| ​                     | `elementIsSelected( element )`                                                                     |
| ​                     | `elementIsVisible( element )`                                                                      |
| ​                     | `elementLocated( locator )`                                                                        |
| ​                     | `elementTextContains( element, substr )`                                                           |
| ​                     | `elementTextIs( element, text )`                                                                   |
| ​                     | `elementTextMatches( element, regex )`                                                             |
| ​                     | `elementsLocated( locator )`                                                                       |
| ​                     | `stalenessOf( element )`                                                                           |
| ​                     | `titleContains( substr )`                                                                          |
| ​                     | `titleIs( title )`                                                                                 |
| ​                     | `titleMatches( regex )`                                                                            |
| ​                     | `urlContains( substrUrl )`                                                                         |
| ​                     | `urlIs( url )`                                                                                     |
| ​                     | `urlMatches( regex )`                                                                              |
| ​                     | `elementTextMatches( element, regex )`                                                             |
| ​                     | `elementsLocated( locator )`                                                                       |
| ​                     | `stalenessOf( element )`                                                                           |
| ​                     | `titleContains( substr )`                                                                          |
| ​                     | `titleIs( title )`                                                                                 |
| ​                     | `titleMatches( regex )`                                                                            |
| ​                     | `urlContains( substrUrl )`                                                                         |
| ​                     | `urlIs( url )`                                                                                     |
| ​                     | `urlMatches( regex )`                                                                              |
| **Reference**         | https://selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/lib/until.html         |

#### Generating Keyboard Events <a href="#generating-keyboard-events" id="generating-keyboard-events"></a>

Representations of pressable keys that aren't text.

| **Namespace**         | `selenium-webdriver`                                                                                 |
| --------------------- | ---------------------------------------------------------------------------------------------------- |
| **Module**            | `Key`                                                                                                |
| **Import Syntax**     | `import { Key } from 'selenium-webdriver';`                                                          |
| **Used Like**         | `await driver.findElement(By.css('.form-input')).sendKeys(Key.RETURN);`                              |
| **Supported methods** | `Key.chord( ...keys )`                                                                               |
| **Values**            | See the reference below                                                                              |
| **Reference**         | https://selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index\_exports\_Key.html |

| **Namespace**   | `thousandeyes`                                                                                                                                                                                                                                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**      | `driver`                                                                                                                                                                                                                                                                                                                        |
| **Method**      | `takeScreenshot()`                                                                                                                                                                                                                                                                                                              |
| **Used Like**   | `await driver.takeScreenshot();`                                                                                                                                                                                                                                                                                                |
| **Description** | Takes a screenshot of the current page and stores it in memory. These screenshots are collected at the end of the test. A maximum of three screenshots is allowed; if this limit is exceeded, new screenshots replace the older ones. Also, by default, a screenshot is taken automatically if a transaction test has an error. |
| **Parameters**  | None                                                                                                                                                                                                                                                                                                                            |
| **Returns**     | None                                                                                                                                                                                                                                                                                                                            |

| **Namespace**     | `thousandeyes`                                                                                                                                                    |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**        | `credentials`                                                                                                                                                     |
| **Import Syntax** | `import { credentials } from 'thousandeyes';`                                                                                                                     |
| **Used Like**     | `credentials.get('MyPasswordName');`                                                                                                                              |
| **Method**        | `get( credentialName )`                                                                                                                                           |
| **Description**   | Gets the stored credential value matching the supplied name. Only works if you have already associated the credential with the current test (Test settings page). |
| **Parameters**    | `credentialName` (string) The name of the credential to fetch                                                                                                     |
| **Returns**       | (string) The password or sensitive value associated with the supplied credential name                                                                             |

You can’t upload a pre-existing file, only a generated one. You can specify the file size and choose text or binary format.

| **Namespace**     | `thousandeyes`                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Module**        | `uploads`                                                                                                                                                    |
| **Import Syntax** | `import { uploads } from 'thousandeyes'`                                                                                                                     |
| **Used Like**     | `await uploads.generateFile('lion-for-marbas.jpeg', fileContent: any, encoding?: string);`                                                                   |
| **Method**        | `generateFile( filename, fileContents )`                                                                                                                     |
| **Description**   | Write a file to the file system with the given filename, and return a path to the generated file that can be referenced when populating a file upload field. |
| **Parameters**    | `fileName` (string) The name of the file to be uploaded.                                                                                                     |
| ​                 | `fileContents` (any) File contents encoded as string.                                                                                                        |

#### Generate a Random Text File <a href="#generate-a-random-text-file" id="generate-a-random-text-file"></a>

| **Namespace**     | `thousandeyes`                                                                                                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**        | `uploads`                                                                                                                                                                           |
| **Import Syntax** | `import { uploads } from 'thousandeyes'`                                                                                                                                            |
| **Used Like**     | `await uploads.generateRandomTextFile(2000, 'myFilename.txt');`                                                                                                                     |
| **Method**        | `generateRandomTextFile( sizeInBytes, fileName )`                                                                                                                                   |
| **Description**   | Create a file of the given size with the given filename, returning a path to the generated file. The generated file will be filled with randomly-generated alphanumeric characters. |
| **Parameters**    | `sizeInBytes` (number) desired byte size of the generated file.                                                                                                                     |
| ​                 | `fileName` (string) The name of the file to be generated.                                                                                                                           |

#### Generate a Random Binary File <a href="#generate-a-random-binary-file" id="generate-a-random-binary-file"></a>

| **Namespace**     | `thousandeyes`                                                                                                                                                    |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**        | `uploads`                                                                                                                                                         |
| **Import Syntax** | `import { uploads } from 'thousandeyes'`                                                                                                                          |
| **Used Like**     | `await uploads.generateRandomBinaryFile(2000, 'myFileName.bin');`                                                                                                 |
| **Method**        | `generateRandomBinaryFile( sizeInBytes, fileName )`                                                                                                               |
| **Description**   | Create a file of the given size with the given filename, returning a path to the generated file. The generated file will be filled with randomly-generated bytes. |
| **Parameters**    | `sizeInBytes` (number) desired byte size of the generated file.                                                                                                   |
| ​                 | `fileName` (string) The name of the file to be generated.                                                                                                         |

For file downloads, you can get the file path, path length, hash, or extract text from a downloaded PDF.

#### Wait for a File to Download <a href="#wait-for-a-file-to-download" id="wait-for-a-file-to-download"></a>

| **Namespace**     | `thousandeyes`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Module**        | `downloads`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Import Syntax** | `import { downloads } from 'thousandeyes';`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Used Like**     | `await downloads.waitForDownload('myFilename.txt', 10 * 1000);`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Method**        | `waitForDownload( fileName, timeout )`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Description**   | Waits for a download matching the supplied filename to appear and then to finish. If a file matching the supplied name has previously been downloaded within the current script, this function will complete immediately. If no file matching the supplied name has been or is currently downloading, it will wait for the supplied timeout amount of time for the file to appear and finish downloading. Downloaded files are saved in a temporary folder on the agent. All files from previous tests are deleted from the temporary folder before a transaction test is run. |
| **Parameters**    | `fileName` (string) The name of the file to wait for                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ​                 | `timeout` (number) The max number of milliseconds to wait for download completion. Defaults to 60 seconds                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

| **Namespace**     | `thousandeyes`                                               |
| ----------------- | ------------------------------------------------------------ |
| **Module**        | `downloads`                                                  |
| **Import Syntax** | `import { downloads } from 'thousandeyes'`                   |
| **Used Like**     | `await downloads.getContents ('myFilePath');`                |
| **Method**        | `getContents ( path )`                                       |
| **Description**   | Return the contents of the specified downloaded file's path. |
| **Parameters**    | `path` (string)                                              |

| **Namespace**     | `thousandeyes`                                           |
| ----------------- | -------------------------------------------------------- |
| **Module**        | `downloads`                                              |
| **Import Syntax** | `import { downloads } from 'thousandeyes'`               |
| **Used Like**     | `await downloads.getSize('myFilePath');`                 |
| **Method**        | `getSize( path )`                                        |
| **Description**   | Return the size of the specified downloaded file's path. |
| **Parameters**    | `path` (string)                                          |

| **Namespace**     | `thousandeyes`                                                                         |
| ----------------- | -------------------------------------------------------------------------------------- |
| **Module**        | `downloads`                                                                            |
| **Import Syntax** | `import { downloads } from 'thousandeyes'`                                             |
| **Used Like**     | `await downloads.getMD5 ('myFilePath');` or `await downloads.getSHA256('myFilePath';`) |
| **Method**        | `getMD5 ( path )` or `getSHA256 ( path )`                                              |
| **Description**   | Return the hash of the specified downloaded file's contents.                           |
| **Parameters**    | `path` (string)                                                                        |
| **Returns**       | ​                                                                                      |

| **Namespace**     | `thousandeyes`                                                                                                                                |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**        | `downloads`                                                                                                                                   |
| **Import Syntax** | `import { downloads } from 'thousandeyes'`                                                                                                    |
| **Used Like**     | `await downloads.getPdfTextContents('myFilePath');`                                                                                           |
| **Method**        | `getPdfTextContents ( path )`                                                                                                                 |
| **Description**   | Extract all text from a downloaded PDF file. You can use this to verify that the contents of a downloaded PDF file matches your expectations. |
| **Parameters**    | `path` (string)                                                                                                                               |

### Measuring Transaction Time(s) <a href="#measuring-transaction-time-s" id="measuring-transaction-time-s"></a>

ThousandEyes transactions support two types of measuring time:

Markers are custom time delimiters, enabling precise time measurements of smaller sections of the transaction. A maximum of 200 markers can be defined in a transaction script. The **Waterfall** tab displays the first ten markers, with a **Show more** link if more than ten markers are defined.

| **Namespace**   | `thousandeyes`                                                                                                              |
| --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **Module**      | `markers`                                                                                                                   |
| **Method**      | `start( markerName )`                                                                                                       |
| **Description** | Starts a marker with the supplied name. This marker can later be stopped by calling the `stop` function with the same name. |
| **Parameters**  | `markerName` (string) The name of the marker                                                                                |
| **Returns**     | None. Will throw an error if attempting to start a previously started marker.                                               |

| **Namespace**   | `thousandeyes`                                                                                                         |
| --------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Module**      | `markers`                                                                                                              |
| **Method**      | `stop( markerName )`                                                                                                   |
| **Description** | Stops the marker matching the supplied name.                                                                           |
| **Parameters**  | `markerName` (string) The name of the marker                                                                           |
| **Returns**     | None. Will throw an error if attempting to stop a marker that hasn't been started yet or one that was already stopped. |

| **Namespace**   | `thousandeyes`                                                                                                                                                                |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**      | `markers`                                                                                                                                                                     |
| **Method**      | `set( markerName )`                                                                                                                                                           |
| **Description** | Creates a marker that spans from transaction start time to the time this method is called. Calling `set` implicitly closes the marker, so there is no need to later close it. |
| **Parameters**  | `markerName` (string) The name of the marker                                                                                                                                  |
| **Returns**     | None.                                                                                                                                                                         |

Running a transaction test implicitly causes the overall transaction time measurement, spanning from the moment the transaction test run starts and to the end of the transaction. However, if customization of overall transaction time's start and stop moments is required, the following methods can be used to such effect. |

Set the overall transaction time **start** moment:

| **Namespace**   | `thousandeyes`                                                                                                           |
| --------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **Module**      | `transaction`                                                                                                            |
| **Method**      | `start()`                                                                                                                |
| **Description** | Sets the start time of the transaction. If not called, the transaction start time will default to the script start time. |
| **Parameters**  | None                                                                                                                     |
| **Returns**     | None                                                                                                                     |

Set the overall transaction time **end** moment:

| **Namespace**   | `thousandeyes`                                                                                                       |
| --------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Module**      | `transaction`                                                                                                        |
| **Method**      | `stop()`                                                                                                             |
| **Description** | Sets the end time of the transaction. If not called, the transaction start time will default to the script end time. |
| **Parameters**  | None                                                                                                                 |
| **Returns**     | None                                                                                                                 |

Provided is a set of mechanisms dedicated to locating elements on the page.

| **Namespace**                | `selenium-webdriver`                                                                                 |
| ---------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Class**                    | `By`                                                                                                 |
| **Import Syntax**            | `import { By } from 'selenium-webdriver';`                                                           |
| **Used Like**                | `await driver.findElement(By.css('#myId'));`                                                         |
| **Supported static methods** | `By.className( name )`                                                                               |
| ​                            | `By.css( selector )`                                                                                 |
| ​                            | `By.id( selector )`                                                                                  |
| ​                            | `By.js( script, ...var_args )`                                                                       |
| ​                            | `By.linkText( text )`                                                                                |
| ​                            | `By.name( name )`                                                                                    |
| ​                            | `By.partialLinkText( text )`                                                                         |
| ​                            | `By.xpath( xpath )`                                                                                  |
| **Reference**                | https://selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/lib/by\_exports\_By.html |

The `assert` module provides a set of assertion functions for verifying invariants.

**NOTE:** Only strict mode is supported.

| **Namespace**         | `assert`                                                                         |
| --------------------- | -------------------------------------------------------------------------------- |
| **Module**            | `assert`                                                                         |
| **Import Syntax**     | `import assert from 'assert';`                                                   |
| **Used Like**         | `assert(url === 'https://wikipedia.org', 'Assertion failed: not on wikipedia!')` |
| **Supported methods** | `assert( value[, message] )`                                                     |
| ​                     | `deepEqual( actual, expected[, message] )`                                       |
| ​                     | `doesNotReject( asyncFn[, error][, message] )`                                   |
| ​                     | `doesNotThrow( fn[, error][, message] )`                                         |
| ​                     | `equal( actual, expected[, message] )`                                           |
| ​                     | `fail( [message] )`                                                              |
| ​                     | `ifError( value )`                                                               |
| ​                     | `notDeepEqual( actual, expected[, message] )`                                    |
| ​                     | `notEqual( actual, expected[, message] )`                                        |
| ​                     | `ok( value[, message] )`                                                         |
| ​                     | `rejects( asyncFn[, error][, message] )`                                         |
| ​                     | `throws( fn[, error][, message] )`                                               |
| **Reference**         | https://nodejs.org/api/assert.html                                               |

Use the `authentication` module to get a time-based one-time password (TOTP) for 2-factor authentication, as in this scripting example:

[usingTOTPTwoFactorAuth.js](https://github.com/thousandeyes/transaction-scripting-examples/blob/master/examples/usingTOTPTwoFactorAuth.js)

.

| **Namespace**     | `thousandeyes`                                                                                                                                                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module**        | `authentication`                                                                                                                                                                      |
| **Import Syntax** | `import { authentication } from 'thousandeyes'`                                                                                                                                       |
| **Used Like**     | `var totp = authentication.getTimeBasedOneTimePassword(secretToken);`                                                                                                                 |
| **Method**        | `getTimeBasedOneTimePassword( secretToken )`                                                                                                                                          |
| **Description**   | Generates a 6-digit temporary authentication code to be used in conjunction with a password on sites that support 2 factor authentication with time-based one-time passwords (TOTPs). |
| **Parameters**    | `secretToken` (string) Secret token provided by Identity administrator.                                                                                                               |
| **Returns**       | (string) One-time password.                                                                                                                                                           |

For further information about transaction testing, refer to the collection of documentation pages under

[Transaction Tests](broken-reference)

.
