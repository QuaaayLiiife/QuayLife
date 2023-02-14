# Using the Transactions (Classic) View

| Notice of Obsolescence                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>This content is related to an older generation of ThousandEyes transaction test type, now renamed to <strong>Transaction (Classic)</strong>. We encourage you to start using the more powerful, JavaScript-based current generation of transactions. For more information about the current generation transaction testing, head over to the</p><p><a href="https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/transaction-scripting-reference.md">Transaction Scripting Guide</a></p><p>.</p> |

A Web Transaction test is a kind of page load test, where agents running the tests attempt to load a web page in a real browser, then interact with that page using a predefined script, written in Selenium. When you create any Web Transaction test, you get access to the Transactions View. The Transactions View leverages the

[ThousandEyes standard layout](https://github.com/thousandeyes/docs/blob/prod/product-documentation/archived-documentation/thousandeyes-view-layouts.md)

.

This article highlights specifics shown in the Web Transactions view.

The example below is based on the following script:

| 1. | Open LSE homepage                  | open              | /                                                                                                                                                                                 | ​     |
| -- | ---------------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| 2. | Enter "aapl" into search input box | typeKeys          | xpath=//input\[@id="head\_solr\_search\_input"]                                                                                                                                   | aapl  |
| 3. | Wait for the autosuggestion        | waitForCondition  | selenium.isElementPresent('xpath=//li\[@class="ui-menu-item"]/a/div/span\[text()="Aapl"]') && selenium.isVisible('xpath=//li\[@class="ui-menu-item"]/a/div/span\[text()="Aapl"]') | 5000  |
| 4. | Click the autosuggestion           | click             | xpath=//li\[@class="ui-menu-item"]/a/div/span\[text()="Aapl"]                                                                                                                     | ​     |
| 5. | ​                                  | waitForPageToLoad | ​                                                                                                                                                                                 | 15000 |

The screenshot below shows the result of a regionally distributed Web Transaction test to

[https://www.londonstockexchange.com/](https://www.londonstockexchange.com/)

, searching for "AAPL" stock symbol and verifying that the resulting page loads.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-54d7d5a946f2d2c05ee9ddf4da10fbba97f20226%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-1.png?alt=media)

Transaction tests offer a single view, the Transactions view. Below are the view-specific options.

A given metric display changes depending on whether an agent location is selected.

*
  * With no agent selected: average percentage of total steps completed successfully.
  * With an agent selected: percentage of steps completed successfully by that agent. Each line of the transaction is numbered, starting from 0 (opening the starting page).
*
  * With no agent selected: average time for transaction completion - only locations where the transaction completes successfully are used in this calculation.
  * With an agent selected: the time required to complete the transaction, if completed successfully.

The **View Script** link displays the steps of the script. The contents of the **Value** field are not shown if they contain text, which could represent passwords or other sensitive information. Those fields instead display asterisks (\*\*\*\*\*\*).

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-691302a59d1cde90b2f653c7581b8321c0e3fb36%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-2.png?alt=media)

Unlike other views, this section is fairly static. It includes the completion percentage and transaction time. As with other views, the data is either calculated using global averages, or from a single agent location, depending on whether or not an agent is selected.

*   **Map** tab of the **Transaction** view without a location selected

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a2ffccc1c91faeae963e9d756d3cc9109bf1aece%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-3.png?alt=media)

    ​
*   **Map** tab of the **Transaction** view with a location selected

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e9b4f5a29b7e593674e7a07dfe938b2c54c27cf3%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-4.png?alt=media)

    ​

The **Table** tab of a Transaction View displays a list of agents, the date of the measurement in the user's chosen time zone, the completion of the test (percentage, number of steps complete out of total steps), and the transaction time for those steps.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-072484168098503c31b15e114d92d9f7e2735f20%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-5.png?alt=media)

The **Timing** tab of a Transaction View has two histogram graphics. The histogram on the left half of the page lists each transaction step by name and the time for each step. The histogram on the right half of the page lists each page by URL and the time for each page. Mouse over a histogram bar to display the timing information in a tooltip. Click a histogram bar to switch to the **Waterfall** tab with the relevant page's waterfall displayed. Or click a step or page name to make the switch to the **Waterfall** tab.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-becf589733ff0a8cafe1aa5c4bb212fdf09633ff%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-6.png?alt=media)

The **Waterfall** tab displays listings of objects loaded on each page and data associated with the loading of each object, along with data on the loading of the total page, for each page loaded. The itemized view and the list below describe the features on this tab.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1a69fa1b35c4a28e7b9b726b6f64116f1ec028f0%2Fproduct-documentation\_thousandeyes-basics\_using-the-transactions-classic-view-7.png?alt=media)

1.  1\.

    **Page info:** The page title is shown, along with the URL of the page accessed.
2.  2\.

    **Page number banner:** To change the context of the waterfall to show a single page, click the page number in the banner. The size of the block for each page is proportional to the fraction of time spent on that page, relative to the total transaction time.
3.  3\.

    **Page boundaries:** Along with #4, change the bounds to select the pages shown in the waterfall. Pull the left boundary to the right, and the right boundary to the left.
4.  4\.

    See #3 above. In the example above, we're showing all four pages' worth of data.
5.  5\.

    **Navigation buttons:** Use the Left, Right and "Show All" buttons to change the context of what is being shown. For example, where a single page is selected, the left and right buttons will change the selection to the previous and next page (respectively) in the transaction.

    By default, the transaction will show each page visited starting with the start step and ending with the end step, as defined in the transaction script. If a single page is selected, that page's DOM and page load times will be shown as normal using the red and blue vertical bars transiting the waterfall. If the content being shown has multiple pages, the DOM and page load times will not be shown.
