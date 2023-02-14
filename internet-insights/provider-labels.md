# Provider Labels

Provider labels are a quick way to pre-select the providers you care about, in order to surface those providers when viewing data coming from Internet Insights. As with other types of labels for tests and agents, provider labels are customer-defined and are visible within your account group.

After defining provider labels in **Internet Insights > Catalog Settings** on the **Labels** tab, you can use these labels on the Internet Insights pages, as well as in alert rules and when creating custom dashboards. Labels are also visible in the Internet Insights packages and provider listings.

### Use Cases for Provider Labels <a href="#use-cases-for-provider-labels" id="use-cases-for-provider-labels"></a>

**Simple:** A customer wants to see only the providers that they care about, so they create a provider label called “primary providers” and select that one label as a filter wherever Internet Insights data is shown.

**Multiple branch offices:** A bank or financial institution has around 20 locations that represent major branch offices in different cities around the world. For example, a New York headquarters might have 2-3 providers, including 1-2 backup providers for failover. One way to use provider labeling would be a “tier 1 providers” label for the primary providers, and a “tier 2” for the other ones, or to use separate provider labels by region depending on whether the branches use the same providers or not.

**Provider evaluation:** A brick-and-mortar retailer with outlets and distribution centers throughout North America wants to diversify their infrastructure. They are evaluating a number of potential providers as backups or failovers for better disaster preparedness. They might create one label called “existing providers” and another for “potential providers” and then create a complex dashboard with dozens of widgets side by side, in order to compare the two provider groups. They can then update this entire dashboard just by editing a label.

### Where Can I Use Provider Labels? <a href="#where-can-i-use-provider-labels" id="where-can-i-use-provider-labels"></a>

Specifically, provider labels are available in the following areas of the ThousandEyes platform:

* On the **Internet Insights > Overview** map, you can filter by **Affected Provider**.
* On the **Internet Insights > Views** screen at the top, you can click **Add a Filter**, choose **Affected Provider**, and then choose one or more provider labels.
* On the **Internet Insights > Catalog Settings** tabs for **Packages** and **Providers**, if the same provider or package has multiple labels associated, hover over the label icons to see the label names.
* On the **Alerts > Alert Rules** screen, on the **Internet Insights** tab, you can quickly set up alert rules for all your favorite providers. Under **Settings**, change the Catalog Providers option to **Specific** in order to see the providers on the drill-down at the bottom.
* On both **Reports** and **Dashboards**, any widget that includes Internet Insights as a data source. Fill out the top options in order to see the drill-down options for Catalog Providers with the provider labels.

### Creating and Editing Provider Labels <a href="#creating-and-editing-provider-labels" id="creating-and-editing-provider-labels"></a>

Use the **Labels** tab in **Internet Insights > Catalog Settings** to add or edit provider labels. You need permission to edit labels as described in

[Managing Roles](https://docs.thousandeyes.com/product-documentation/user-management/rbac/role-based-access-control-explained#managing-roles)

in order to create or modify provider labels.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5f1d01c8ef076b1cf2ddd6702c460db28b5ed62a%2Fprovider-labels-001-create-label.png?alt=media)

To create a new provider label:

1.  1\.

    Go to the **Internet Insights > Catalog Settings** page.
2.  3\.

    Click the **Add New Label** button.
3. 4\.
   * Choose a label display color.
   * Select catalog providers. Use the Search box to find providers by name.

To edit an existing provider label, go to the **Labels** tab, click the row of the label you want to edit, make your changes in the side panel and click **Save**.

On the **Labels** tab, where all the labels are listed, use the ellipsis menu to **Duplicate** or **Delete** a provider label, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a3203e95be4decb58fdc8c69a9bec47d28e81940%2Fprovider-labels-002-duplicate-or-delete-label.png?alt=media)

### Viewing Provider Labels in the Catalog <a href="#viewing-provider-labels-in-the-catalog" id="viewing-provider-labels-in-the-catalog"></a>

To view the label names that are associated with providers and packages, go to **Internet Insights > Catalog Settings** and hover over the label icon for the list entry, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-02fcbf947bcacb1c81332bd3084e7ffd8ebc5846%2Fprovider-labels-003-viewing.png?alt=media)

This section describes how to use provider labels from Internet Insights in other parts of the ThousandEyes platform.

#### Filtering by Provider Labels on Overview <a href="#filtering-by-provider-labels-on-overview" id="filtering-by-provider-labels-on-overview"></a>

On **Internet Insights > Overview**, use the **Affected Provider** filter at the top of the screen, as shown in the image below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a95f01dc7b98e8b0ee010cf9934eae2937c20ee0%2Fprovider-labels-004-overview-map.png?alt=media)

To filter the Internet Insights Overview map by provider label:

1.  1\.

    Choose **Internet Insights > Overview**.
2.  2\.

    Click **Affected Providers** at the top.
3. 3\.
   * Use the checkboxes on the right to select from provider labels that you have created. The list updates to show only providers that match your label selections.
   * Expand the list of providers on the left and choose the providers to show.
4.  4\.

    Click elsewhere on the screen to close the pop-out panel.

If you don’t see any provider labels, it means that your organization hasn’t configured any labels for your account group.

#### Filtering by Provider Labels on Views <a href="#filtering-by-provider-labels-on-views" id="filtering-by-provider-labels-on-views"></a>

On the **Internet Insights > Views** screen, the **Affected Provider** filter is available on both Network and Application outages view layers.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f6aaacf37ef062cdcbf2808815255dd773b5b39b%2Fprovider-labels-005-views-filter.png?alt=media)

To filter the Internet Insights Views by provider label:

1.  1\.

    Choose Internet Insights > Views.
2.  2\.

    At the top, click Add a filter and choose Affected Providers.
3. 3\.
   * Use the checkboxes on the right to select from provider labels that you have created. The list updates to show only providers that match your label selections.
   * Expand the list of providers on the left and choose the providers to show.
4.  4\.

    Click elsewhere on the screen to close the pop-out panel.

#### Using Provider Labels in Alert Rules <a href="#using-provider-labels-in-alert-rules" id="using-provider-labels-in-alert-rules"></a>

Provider labels are available in the alert rules for Internet Insights only.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0c5c8f7d7fc4a5a9be22526790912f6698f24c79%2Fprovider-labels-006-alert-rules.png?alt=media)

To create an alert rule using provider labels:

1.  1\.

    Choose **Alerts > Alert Rules**.
2.  2\.

    Click the **Internet Insights** tab.
3.  3\.

    Click **Add New Alert Rule** in the upper right.
4.  4\.

    In the pop-out panel, choose an Alert Type and enter a rule name.
5.  5\.

    Change the **Catalog Providers** from Any to **Specific**.
6.  6\.

    Click the provider selection drop-down.
7.  7\.

    Select one or more provider labels from the checkboxes on the right.
8.  8\.

    Select the providers to include in the alert rule in the checkboxes on the left.

#### Using Provider Labels on Dashboards and Reports <a href="#using-provider-labels-on-dashboards-and-reports" id="using-provider-labels-on-dashboards-and-reports"></a>

One way to use provider labels on dashboards is to set up side-by-side comparisons with different provider groups. You can create a widget and then duplicate it and use a different provider label, without having to hand-select preferred providers each time.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1683c7b88f93adb4e2523b053cc1cd2583cb0f58%2Fprovider-labels-007-dashboard.png?alt=media)

To use provider labels when creating dashboard:

1.  2\.

    Open or create a dashboard and click **+ Add Widget**. Choose a widget type that supports Internet Insights.
2. 3\.
   * Choose **Internet Insights** as the data source.
   * Make selections for Category and Metric, as well as other items such as Measure.
   * In the section titled **DRILL DOWN**, choose **Catalog Providers** and then use the provider selector to choose providers using labels. You can add more filters if desired.

Provider type designations such as SaaS and SECaaS are used in ThousandEyes to separate out the provider packages on the Packages tab in Internet Insights > Catalog Settings. The provider type can affect visibility in the Internet Insights views when switching between Network Outages and Application Outages, since not all provider types show up in both places.
