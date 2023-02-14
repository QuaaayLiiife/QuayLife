# Configuring Internet Insights

In order to use the collective intelligence of Internet Insights, you’ll need to subscribe to one or more packages. Without packages, you’ll still see limited data in Internet Insights – but only for your own tests. If your license includes a specified number of packages, you’ll still need to choose which packages to activate, and ensure that all your package licenses have been actively applied.

A _package_ is a collection of Internet Insights providers (formerly known as catalog entries) with the same provider type and region. Customers license a package in order to display outages involving any of the providers included in the package. An example of a package would be Asia/Pacific CDN Providers, which includes a list of providers like Amazon Cloudfront and Akamai, but in the Asia/Pacific region.

To review and activate packages, go to **Internet Insights > Catalog Settings**.

Unused licenses still incur subscription fees. Therefore, ensure that all your package licenses have been applied to packages.

To activate a package for Internet Insights when you have available licenses for it:

1.  1\.

    Go to **Internet Insights > Catalog Settings** screen and click the **Packages** tab.
2.  2\.

    Verify that the **Available** counter shows one or more licenses.
3.  3\.

    Find the row with the package that you want to add.
4.  4\.

    In the **Included** column, click the **Active** slider to add the package.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b55f1f450ec8aaaee110bc2244951c9c367bf88a%2Finternet-insights-013-catalog-packages-tab.png?alt=media)

Sometimes you'll need to optimize your package usage, for example to transfer an existing package license to a package that better reflects your monitoring needs. In order to do this you'll first need to de-activate a package, and then add (activate) the desired package in its place. To remove an Internet Insights package, hover over the row with the package to be removed, and change the **Active** slider to off. You can also add and remove packages from the **Providers** tab in a similar way.

Both the **Packages** and the **Providers** tabs in **Internet Insights > Catalog Settings** have interactive coverage maps with information about what is included in each package or provider region. The example below shows a coverage map for the package titled “Asia/Pacific CDN Providers.”

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-661866deaa959753e629245ed73eab6a602fd8ae%2Finternet-insights-015-catalog-packages-map.png?alt=media)

The map lets you choose other providers from the drop-down selector list at the top. Hover over a location to see interface details for the indicated location.

The **Providers** tab shows a coverage map for each provider by region.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-134e2447e631b4fbfcb8128ef089aebbbb1ca0cc%2Finternet-insights-016-catalog-providers-map.png?alt=media)

There’s a difference in what you can see with your own tests when they are affected by outages, vs. the macro-scale Internet outages that are visible with Internet Insights package coverage. Whenever one of your tests is affected by an outage, you will see the complete outage affecting that test, but you won’t see other outages for that same region or provider type, even if those other outages might be affecting visibility to the same target as the one in your test.

Service provider types for Internet Insights packages include the following:

* CDN - Content Delivery Network provider
* IAAS - Infrastructure as a Service providers
* ISP - Internet Service Providers
* SAAS - Software as a Service providers
* SECAAS - Security as a Service providers
* UCAAS - Unified Communications as a Service providers

Each Internet Insights provider catalog entry includes the following:

* Provider type, such as SaaS, DNS, or ISP
* Number of associated Autonomous System Numbers (ASNs) for providers who use public networks not associated to their ASNs

Each package includes multiple provider catalog entries. So to gain access to outage information for a particular provider in a particular geographic region, find the package with this provider in it and subscribe to the package.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bc5f966498f15b1e78dae4d94f1f625e03360f12%2Finternet-insights-014-catalog-providers-tab.png?alt=media)

The geographic regions for Internet Insights packages are:

* Europe, Middle East, and Africa (EMEA)

### How Internet Insights is Licensed <a href="#how-internet-insights-is-licensed" id="how-internet-insights-is-licensed"></a>

Internet Insights outage data is provided to ThousandEyes customers who have an Internet Insights subscription. In addition to the basic Internet Insights subscription, ThousandEyes displays outages according to the Internet Insights packages that you have licensed.

* Base (included): Outages are displayed in providers that affect one or more of your tests.
* Packages: Outages are displayed in providers from licensed packages.

Internet Insights automatically displays outages that affect your enabled tests. To configure Internet Insights, select the desired packages.

For Internet Insights, you purchase one or more _package licenses_. A package license allows you to select a package - for example, the **North America ISPs** package. You can purchase multiple licenses, up to the number of available packages.

Licenses are not fixed to a given package. You can change the package associated with your license at any time. The number of purchased licenses and the number of licenses currently available to use for a package are displayed at the top right of of the Packages tab on the **Catalog Settings** page.

Each day, you can make changes to a maximum number of Internet Insights packages equal to the number of Internet Insights package licenses that you’ve purchased. Each “change” equals one on/off event, as in turning one package off and then turning another one on. If you exceed this limit you won't be able to make package changes again until the following day. In this case, “daily” means “a rolling 24-hour window”.

ThousandEyes allows these changes so that you can activate different packages if your long-term visibility needs change. This capability should not be relied upon to make frequent changes.

### Determining Which Packages to Activate <a href="#determining-which-packages-to-activate" id="determining-which-packages-to-activate"></a>

To determine which packages to license, consider the services that you need to monitor, and any existing ThousandEyes tests you have already configured to monitor those services. Based on those factors, you can determine whether your existing tests provide sufficient coverage to identify outages, or if you need one or more packages to ensure visibility into outages.

For example, a single HTTP server test to a web app hosted in a single data center, run from large numbers of Cloud and/or Enterprise Agents in many different providers is likely to have paths that cross many providers, including the Internet service provider(s) for the data center. An outage in any of the traversed providers will be displayed without your needing to subscribe to a package containing the specific providers.

In contrast, a web app that is hosted in many geographic regions may require subscribing to one or multiple packages, rather than relying on the HTTP server test.

Keep in mind the following considerations:

* If the app or service that you want to monitor is hosted by a single provider, select the package(s) that include that provider.
  * For example, the package titled “North America IAAS Providers” is for a Provider Type of "IAAS" and includes such providers as Microsoft Azure, Amazon Web Services, and Rackspace.
  * Note that some providers appear under both Network and Application, but they’ll be monitored somewhat differently depending on whether you want to focus on a single application, or on anything impacted by the provider’s infrastructure.
* Depending on the geographic distribution of the app's users, select one or more of the catalog regions. For example, the "North America IAAS Providers" package, the "Asia/Pacific IAAS Providers" package, and so on.
* If the same app is hosted by multiple providers, check to see if there’s an application package for it. Note that applications can be SaaS, or sometimes UCaaS or IaaS.
* If the application is on multiple providers and there isn’t a ThousandEyes application package that provides sufficient coverage, determine whether the multiple providers are all of the same type (for example, CDN or IAAS) and in the same region (for example, North America or Asia Pacific).
  * If the providers are of the same type and in the same region, no additional packages are needed.
  * If type, region, or both are not identical, you may need additional packages, depending on the hosting locations of the providers.

#### Tips for Choosing Packages <a href="#tips-for-choosing-packages" id="tips-for-choosing-packages"></a>

* Even if you already have ThousandEyes tests running for a specific application or provider, additional packages (for example, those of Provider Type "ISP") may be beneficial, in order to detect outages outside of the app provider(s) own networks.
*   You can search for specific providers from the **Providers** tab under **Internet Insights > Catalog Settings**. In the example shown below, the search for provider Limelight displays Limelight's catalog entries:

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e37adf34e781c0d0338283cb67bcea456932d398%2Finternet-insights-017-catalog-search-for-provider.png?alt=media)
* On the **Packages** and **Providers** tabs, when you click a listed item, a side panel opens, showing a coverage map for that package or entry (i.e., which networks are included and which geographical location they give visibility into). The coverage map can help you decide which packages to choose.

### Provider Types and Labels on Internet Insights View Screens <a href="#provider-types-and-labels-on-internet-insights-view-screens" id="provider-types-and-labels-on-internet-insights-view-screens"></a>

For Internet Insights view screens, there are 7

[provider types](broken-reference)

but some are only visible under Application Outages, while others only appear under Network Outages. Coverage is partially determined by the type of data that is obtainable from that provider through ThousandEyes tests.

For example, ThousandEyes needs to have certain network data in order to include that provider under Network Outages. And if a provider is purely an application, such as Adobe Creative Cloud, that provider won’t appear under Network Outages.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4422c4f974072b74ca52c394138647a37467dc26%2Finternet-insights-018-provider-types.png?alt=media)

The provider coverage shown in the figure is subject to change, as ThousandEyes is constantly making improvements.

The system-configured provider type coverage means that:

* You won’t see application providers on the **Network Outages** view screen, even if your provider label includes them and you’ve added that provider label as a filter. The filters can only select from what’s already there.
* On the **Network Outages** view, you’ll see all provider types except SaaS, but on the **Application Outages** view, you’ll only see providers that are categorized as IaaS, SaaS, or UCaaS. ISPs such as Limelight will only show up on the Network Outages view.

What if the same name-brand provider offers more than one type of service? In this case, the catalog **Providers** tab lists them as separate providers for each type of service and region. For example Google Workspace is provider type SaaS, while Google/GCP is provider type IaaS.
