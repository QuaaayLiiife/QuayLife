# Monitoring Webex Meetings with Cloud and Enterprise Agents

import { By, Key } from 'selenium-webdriver';

import { driver, browser, markers } from 'thousandeyes';

async function runScript() {

// Navigate to Webex Global Status Page

await driver.get('https://status.webex.com/service/status?lang=en\_US');

await driver.takeScreenshot();

// Find the card for Webex Meetings

let webex\_meetings = await driver.findElement(By.xpath(\`//\*\[text()="Webex Meetings"]\`));

// click on webex meetings to show operational status

await webex\_meetings.click();

// Scroll the card into view and take a screenshot

await driver.executeScript("arguments\[0].scrollIntoView({block: 'center'});", webex\_meetings);

await driver.takeScreenshot();

// Find all the list items showing each component's status

let items = await webex\_meetings.findElements(By.xpath('./../..//li'));

// Iterate over each list item...

await Promise.all(items.map(async function (item) {

let component = await item.findElement(By.css('span.text-secondary')).getText();

let status = await item.findElement(By.css('span.font-body-small')).getText();

console.log((await component), (await status));

// ...and throw an error if any Webex Meeting Comopnent is non-Operational

if (status != 'Operational') {

throw Error('Component "' + component + '" is not operational: ' + status);

async function configureDriver() {

await driver.manage().window().setRect({

await driver.manage().setTimeouts({

implicit: 7 \* 1000 // If an element is not found, reattempt for this many milliseconds

async function configureDriver() {

await driver.manage().setTimeouts({

implicit: 7 \* 1000, // If an element is not found, reattempt for this many milliseconds

async function click(selector) {

await simulateHumanDelay();

const configuredTimeouts = await driver.manage().getTimeouts();

const clickAttemptEndTime = Date.now() + configuredTimeouts.implicit;

await reattemptUntil(attemptToClick, clickAttemptEndTime);

async function attemptToClick() {

await driver.findElement(selector)

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

async function typeText(value, selector) {

await simulateHumanDelay();

const element = await driver.findElement(selector);

await element.sendKeys(value);
