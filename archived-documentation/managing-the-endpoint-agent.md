# Managing the Endpoint Agent

Once you've started collecting data, you can control which machines collect data and send it to ThousandEyes for analysis. Go to

[**Endpoint Agents > Agent Settings**](https://app.thousandeyes.com/endpoint/agent-settings/?section=agents)

Endpoint Agents. This screen allows you to search for existing agents, using either agent name (which defaults to _\[user name] - \[host name])_, or by hostname directly.

#### Disabling an Endpoint Agent <a href="#disabling-an-endpoint-agent" id="disabling-an-endpoint-agent"></a>

An Endpoint Agent can be either enabled or disabled. When enabled and when inside a monitored network, the Endpoint Agent collects performance information for monitored domains. When disabled, the Endpoint Agent still checks in with ThousandEyes every 15 minutes for configuration changes and Endpoint Agent updates. No other information is collected while an Endpoint Agent is disabled. A newly enabled agent's state is reflected in the list immediately, but the agent will receive the updated configuration within 15 minutes (the next time it checks in).

To disable an Endpoint Agent, find the agent in the list, expand it and click the **Disable** button (on the lower left of the expanded Endpoint Agent details panel):

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-61c385ef86a105672512807a6a33a2dc240376a4%2Fproduct-documentation\_endpoint-agent\_configuring-endpoint-agent-setup-4.png?alt=media)

Once disabled, the agent's list entry will show the word "Disabled" in the **Last Contact** column and the aforementioned **Disable** button will become an **Enable** button. This change takes effect immediately.

#### Deleting an Endpoint Agent <a href="#deleting-an-endpoint-agent" id="deleting-an-endpoint-agent"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a9c8d34f24ed2f65133a88268821ad434f63dd9a%2Fproduct-documentation\_endpoint-agent\_configuring-endpoint-agent-setup-5.png?alt=media)

1.  1\.

    Click the options button (

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b9669536ab628c3dc5c968664386c2d502037ecb%2Fproduct-documentation\_endpoint-agent\_configuring-endpoint-agent-setup-6.png?alt=media)

    ) on the Endpoint Agent you wish to delete.
2.  2\.

    Click **Delete.** If the **Delete** option is not available, then your ThousandEyes user account may not have permission to delete Endpoint Agents.
3.  3\.

    Once deleted an Endpoint Agent can be recovered upto 7 days.

Deleting an Endpoint Agent will prevent it from checking in and committing data to our backend services. Normally, administrators should delete Endpoint Agents only to block machines that should not be connecting and sending data to your ThousandEyes account.

#### Reinstalling an Endpoint Agent <a href="#reinstalling-an-endpoint-agent" id="reinstalling-an-endpoint-agent"></a>

If an Endpoint Agent requires reinstallation to address an issue, simply rerun the Endpoint Agent installer, without deleting the existing installation. The most common scenario requiring reinstallation occurs when the Endpoint Agent cannot auto-update itself. Rerunning the installation using the latest installer will update the Endpoint Agent without generating a new agent instance. Such an upgrade will not affect the data continuity.

However, if you do uninstall an Endpoint Agent and then reinstall it again (or select the **Repair** option when running the installer again), the Endpoint Agent will register with the ThousandEyes platform using a new unique Agent ID. Data collected from the new Endpoint Agent instance will not be continuous with the data collected from the older Endpoint Agent instance. Also,

[**Endpoint Agents > Agent Settings**](https://app.thousandeyes.com/endpoint/agent-settings/?section=agents)

**> Endpoint Agents** will display two Endpoint Agent entries with the same name.
