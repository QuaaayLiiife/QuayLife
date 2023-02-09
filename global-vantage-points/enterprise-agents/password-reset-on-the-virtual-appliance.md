# Password Reset on the Virtual Appliance

The ThousandEyes Virtual Appliance can be configured through a web interface which is available at **http://\<IP\_address\_of–Virtual\_Appliance>**. The web interface requires a username and password. The default username and password are:

**Username**: admin **Password**: welcome

The Virtual Appliance installation process will require the password to be changed:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1c51804ddcd30a30505c91361636ef77dbfff4cd%2Fproduct-documentation\_enterprise-agents\_password-reset-on-the-virtual-appliance-4.png?alt=media)

Figure 1: Change Password

### Resetting the Password from the App <a href="#resetting-the-password-from-the-app" id="resetting-the-password-from-the-app"></a>

If the agent is online in the ThousandEyes app, the easiest way to force a password reset is from the

[**Enterprise Agents** tab](https://app.thousandeyes.com/settings/agents/enterprise/?section=agents)

of the **Agent Settings** page:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3d2aff321d1b16c84edeb58655855a91e035bbee%2Fproduct-documentation\_enterprise-agents\_password-reset-on-the-virtual-appliance-1.png?alt=media)

After expanding the agent's row, a **Reset Appliance Password** link appears. Clicking the link will reset the default username and password on the Appliance.

The final step is to log in to the Virtual Appliance's web management page at **http://\<IP\_address\_of–Virtual\_Appliance>** using the default credentials. In the **Access** tab, you will be required to change the password (see Figure 1).

### Resetting the Password from the Hypervisor <a href="#resetting-the-password-from-the-hypervisor" id="resetting-the-password-from-the-hypervisor"></a>

If you can't log in to the Virtual Appliance's web management page, the password can be reset using the Virtual Appliance's console. The console provides a text-driven menu for basic administrative tasks. The console window is a tty device which can be accessed from the hypervisor that is hosting the Virtual Appliance.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cef3bba2a18fdfd6ca04654273e7de776755f275%2Fproduct-documentation\_enterprise-agents\_password-reset-on-the-virtual-appliance-3.png?alt=media)

In the console, press the **R** key to reset the password to the default value.

Next, navigate to the Virtual Appliance's web management page at **http://\<IP\_address\_of–Virtual\_Appliance>** and log in using the default credentials. Upon the initial login, you will be required to change the password (see Figure 1).

NOTE: If the **Current Password** field has been auto-populated, then your browser's password manager has filled the field with a value that may or may not be correct. If you receive an error that the auto-populated password is incorrect, then delete the contents of the **Current Password** and manually enter "welcome", in order to change the password. We strongly recommend disabling password completing for the Virtual Appliance's URLs.
