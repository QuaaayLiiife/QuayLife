# Transaction Scripting Tips and Tricks

### Choosing Better Element Selectors <a href="#choosing-better-element-selectors" id="choosing-better-element-selectors"></a>

The most common optimization for transaction scripting involves making your CSS element selectors simpler and more reliable. Below are some examples of selectors and how to improve them.

To clarify, an element is any item on the page, and a CSS selector is a method of describing said element. The CSS selector could then be a name, category, ID, iframe, etc.

#### Avoid Dynamically Generated IDs <a href="#avoid-dynamically-generated-ids" id="avoid-dynamically-generated-ids"></a>

Some auto-generated selectors will identify an element using an ID that appears to be unique and stable, but that is actually dynamically generated. For example:

await driver.findElement(By.css('#tabZoneId278'));

The element ID `tabZoneId278` is very likely to be a dynamic element ID that was generated by a UI framework, so it may not persist over time.

#### Avoid Overly Specific Selectors <a href="#avoid-overly-specific-selectors" id="avoid-overly-specific-selectors"></a>

In other cases, you'll find the auto-generated selectors will resort to selectors that are overly specific and too reliant on element hierarchies, like the example below:

await driver.findElement(By.Css('#nm-streaming-container > div.streamingNewsContainer.nsw-subscription-type-realTime.defaultTemplates.news-hideInsight.news-hideSentiment.header-auto-resize.news-hideHeader.news-results-item-insight2-shrinked.news-results-item-sentiment-shrinked.nsw-four-columns > div.news-results.news-list-table.newsSection.streamingTopSection > div');

The above example includes three parent-child levels, separated by >, with additional CSS class selectors with a . separator. If possible, find a selector that is simpler while still uniquely identifying the element on the page.

#### Working With Single Page Apps <a href="#working-with-single-page-apps" id="working-with-single-page-apps"></a>

Single page applications (SPAs) often present a challenge. A single-page app dynamically rewrites the current web page as the user interacts with the page, instead of loading a new page every time the user clicks on something. Because the nature of the page is dynamic, generating a transaction script with static/specific selectors to target a specific page element will not consistently work. It is better to target a class, or use something like regex that can select something in a more fluid manner. Here's an example of clicking on the "call" button in Microsoft Teams:

await click(By.css('#app-bar-20c3440d-c67e-4420-9f80-0e50c39693df .icons-filled'));

The problems with the above are that these elements are dynamic and the long strings of random-seeming characters are non-intuitive, and non-human readable​​. This type of random string often indicates a randomly generated selector. The same selector could be different every time that same user connected, or could be different for different device types. General Selector Guidelines Here are some general guidelines and suggestions for selecting robust and simple CSS selectors:

*   For CSS selectors, avoid relying on parent-child selectors as much as possible. This example shows a selector with no children, which is the preferred way to do it:

    await click(By.css('#positions-securityGroup-Equity-collapsed > .sch'));
*   Don't use sleeps. If you find yourself using `await driver.sleep(3000)` because “it just seems to make things work”, review

    [Use Sleeps and Human Delay Sparingly](broken-reference)

    and look for ways to get rid of the sleep if you can.

#### Criteria for Choosing the Right Element Selector <a href="#criteria-for-choosing-the-right-element-selector" id="criteria-for-choosing-the-right-element-selector"></a>

Let’s say you know which page element you want to focus on, and what to avoid doing, but you’re unsure of what to do next. Here’s a simple guideline: Look for an attribute, ID, or class that seems unlikely to change over time.

Find a unique, human-readable ID. For example you might find something like `<button id="continue_button">`. You could use that ID in your transaction script as follows:

await click(By.css(\`#continue\_button\`));

Look for unique class names. For the element that you want to use, is it the only element on the page that uses that class name? If so, you can do something similar to the following:

await click(By.css(".chat-window-textbox"));

Look for unique attribute values, like `<button aria-label="Dismiss">`. This assumes that there’s only one Dismiss button on the page.

await click(By.css(\`\[aria-label="Dismiss"]\`));

**Unique Combination of Type, Class, Value**

Use combinations of element type, class type, and/or attribute values to achieve element uniqueness. For example, the line below identifies an element named `<textBox name="loginfmt">` by element type and attribute value. The element must be a text box, and it must have the name **loginfmt**.

await click(By.css("textBox\[name='loginfmt']"));

Another approach is to use XPath to search for an element by its text value. For example, to identify a button named **Continue** that’s implemented as `<button>Continue</button>`, do the following:

// Click on a \`button\` element with text 'Continue'

await click(By.xpath(\`//button\[text()="Continue"]\`));

**Unique Sibling-Ancestor Combination**

Finding unique selectors based on combinations of siblings or ancestors can often yield simple and reliable results.

await click(By.css(\`\[data-resin-target="primarybutton"] > .btn-content > span\`));

This process of identifying more simple and robust element selectors is the most important process in creating reliable transaction tests. However, it is not the only challenge to address. Let's look at some other common scenarios and issues you'll encounter.

### Use Pause During Playback <a href="#use-pause-during-playback" id="use-pause-during-playback"></a>

After generating the initial script in the ThousandEyes Recorder, the next step is to look for elements during playback.

1.  1\.

    In the Recorder, run your transaction script as recorded.
2.  2\.

    Use the **Recorder Pause** button to pause at the point in your transaction code that you want to identify a particular element.
3.  3\.

    In the Chromium browser that is used with the ThousandEyes Recorder IDE, open the Developer Tools.
4.  4\.

    Click the small arrow and use it to identify the element for which you want to find a selector.

Search for alternative IDs, classes, attributes, or elements that you can use to select the element in question.

#### Waiting for Element State <a href="#waiting-for-element-state" id="waiting-for-element-state"></a>

Beyond searching for and clicking on an element, you might want your script to pause until an element becomes visible. This is common especially with single page apps, where rich content might be loading dynamically from a backend server or datastore. We can use the `driver.wait(until ...)` functions to accomplish this.

Note you'll need to import the `until()` function by doing the following:

import { By, Key, until } from 'selenium-webdriver';

**Wait for a Single Element**

Here's a simple example of waiting for an element called `<div class="tab-zone" name="chart">` to become visible:

await driver.wait(until.elementIsVisible(driver.findElement(By.css('.tab-zone\[name="chart"])));

**Wait for a Group of Elements**

We can also use `wait()` to wait for a group of elements to become visible. For example, we can find all tab-zone elements and then wait for all of them to become visible, as follows:

const elements = await driver.findElements (By.css(".tab-zone"));

const promises = await elements.map((element) => {

return driver.wait(until.elementIsVisible (element));

await Promise.all(promises);

A more compact version of the above is as follows:

const elements = await driver.findElements (By.css(".tab-zone.tab-widget"));

await Promise.all(await elements.map((element) => {

return driver.wait(until.elementIsVisible (element));