# What Is BrowserBot?

The BrowserBot is a component of the agent code that manages page load and transaction tests. This is accomplished through running an instance of the

[Chromium](https://www.chromium.org/)

browser.

On the other hand, HTTP Server tests are using a custom version of

[cURL library](https://curl.haxx.se/)

under the hood and therefore do not need the BrowserBot installed.

### Can I Install BrowserBot onto an Existing Enterprise Agent? <a href="#can-i-install-browserbot-onto-an-existing-enterprise-agent" id="can-i-install-browserbot-onto-an-existing-enterprise-agent"></a>

Yes. To install the BrowserBot component on an existing Enterprise Agent that does not already have it installed, simply re-run the installation script, including your ThousandEyes Account Group token, and the `-b` flag:

sudo ./install\_thousandeyes.sh -b {your account group token}

This will install the BrowserBot and all required dependencies. The BrowserBot version information will now appear in the Enterprise Agent's **General Info** panel in the

[Cloud & Enterprise Agents > Agent Settings](https://app.thousandeyes.com/settings/agents/enterprise/?section=agents)

page, as per the image below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7fd07b54a4710b46734587dafeed79f98bd54b88%2Fproduct-documentation\_enterprise-agents\_what-is-browserbot-1.png?alt=media)

### Additional Hardware Resource Requirements <a href="#additional-hardware-resource-requirements" id="additional-hardware-resource-requirements"></a>

### Which Version of Chromium Is BrowserBot Using? <a href="#which-version-of-chromium-is-browserbot-using" id="which-version-of-chromium-is-browserbot-using"></a>

There are two methods of determining the Chromium version used:

Pick any Page Load or Transaction test that has headers collection enabled. Open the results view, select one of the agents, switch to the **Waterfall** tab and click on one of the entries' **Headers** link:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-598d5b015186c05a842db0d6af6192da4e59f1d4%2Fproduct-documentation\_enterprise-agents\_what-is-browserbot-2.png?alt=media)

Once there, open the **Request Headers** tab and search for the `user-agent` (or `User-Agent` if HTTP protocol version 1.1 was used) header:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cc51d9169a0ea2f196c56aa5b97f2a76bfd39ff2%2Fproduct-documentation\_enterprise-agents\_what-is-browserbot-3.png?alt=media)

Notice the browser version specified in the specified request header.

#### Method 2 - Inspecting the Installed Package Version <a href="#method-2-inspecting-the-installed-package-version" id="method-2-inspecting-the-installed-package-version"></a>

Once you have connected to the agent's SSH console, a simple command suggests the version of Chromium browser used under the hood. For connecting to the SSH console of appliances, we have guides available for

[Windows](https://docs.thousandeyes.com/product-documentation/enterprise-agents/connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows)

and

[OS X / Linux](https://docs.thousandeyes.com/product-documentation/enterprise-agents/connecting-to-the-thousandeyes-virtual-appliance-using-ssh-mac-linux)

workstation operating systems.

For Ubuntu-based operating systems (including ThousandEyes Virtual Appliances), use the following command:

$ dpkg -l | grep te-chromium

ii te-chromium 68.0.3440.83-1\~bionic amd64 web browser

For RHEL/CentOS/Oracle Linux systems, use the following:

$ rpm -qa | grep te-chromium

te-chromium-68.0.3440.83-1\~centos7.x86\_64

The commands above will return the name of the package installed and by naming convention that is the version of the browser installed. In the example above, the browser version is `68.0.3440.83` - the `-1` suffix is not part of the browser version information - it is a package release number.

The following resources provide further information about related subjects:
