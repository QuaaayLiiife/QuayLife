# Connecting to the ThousandEyes Virtual Appliance Using SSH (Windows)

In order to access the command line of a ThousandEyes Virtual Appliance or Physical Appliance, the Appliance can be configured with one or more SSH public keys. An SSH client configured with the corresponding SSH private key can then log into the Appliance's command line.

This article provides instructions for users of a Microsoft Windows operating system to perform the following steps:

1.  3\.

    Configure the ThousandEyes Appliance

An SSH application such as PuTTY is required. Download the latest

[PuTTY installer](http://www.chiark.greenend.org.uk/\~sgtatham/putty/download.html)

(normally the 64-bit MSI) to install the PuTTY suite of programs, most relevantly:

* PuTTY (**putty.exe**): An SSH client
* PuTTYgen (**puttygen.exe**): An SSH key generator
* (Optional) PSCP (**pscp.exe**): A command-line Secure Copy Protocol client, for copying files from the Appliance

Run the MSI installer to installer once the MSI file has been downloaded. Alternatively, individual executables may be downloaded separately from the PuTTY site.

If you don't already have an SSH key pair (public key and matching private key), you'll need to generate one using PuTTYgen. Open the PuTTYgen program, and follow the steps below.

1.  1\.

    In the **PuTTY Key Generator** window, select the RSA key option and then click the **Generate** button:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-52ef7c1ceacbf47502cd3f6b26a7db2c6309973f%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-1.png?alt=media)

1.  1\.

    Move your mouse back and forth inside the **Key** field to generate randomness.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-26c97334fb46933876ab2a92e0420393e40efad5%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-2.png?alt=media)

1.  1\.

    (Optional) Add a passphrase using the fields provided, if desired.
2.  2\.

    Highlight the public key and copy to the clipboard:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f0292fcc0fb1df2e71452314caaca73c65ceb3c2%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-4.png?alt=media)

1.  1\.

    Save your public and private keys using the **Save public key** and **Save private key** buttons. Note the directory or directories where you save the keys. You'll need the path to the private key for the PuTTY SSH client.

### Configure the ThousandEyes Appliance <a href="#configure-the-thousandeyes-appliance" id="configure-the-thousandeyes-appliance"></a>

The public key of a user's SSH key pair must be present on each agent that is to be accessed. Log into the web interface of a ThousandEyes Appliance, then follow the steps below to configure the Appliance with your public key.

1.  1\.

    On the **Appliance Access** tab, paste the key that was copied in step 4 of the **SSH key creation** section into the **Add New SSH key** field.

NOTE: When pasting the key, make sure the string `ssh-rsa` that prepends the key is present, or the key won't be accepted as valid (see the screenshot below for the correct format of the key).

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0935391ff417f76dca57b90256ce336ae629a367%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-5.png?alt=media)

2\. Click **Add Key**.

The key will be added with the identifying string that follows the key:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-43095fa67804b8f8f883dec407d822fdd4ce26b6%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-6.png?alt=media)

If the key addition fails, most failures are caused by unnecessary beginning and ending lines, comment fields or carriage returns/line feeds. For example, the file saved by the PuTTY Key Generator contains beginning and ending lines and comment fields that need to be removed in order to have a valid public key format:

\---- BEGIN SSH2 PUBLIC KEY ----

Comment: "An RSA SSH key key example"

AAAAB3NzaC1yc2EAAAABJQAAAQEAgXp4D3V6OGVv24Anh2P4Uh1N1KZ+DP9oT3sx

E8U9MybSho1ev4eZuwso2q3M0tC1YU+PQu1RFd0hzZdcS8zTg7+soopI9HRaOoSL

p5IyywDC28AvoJE8q9DtKZoKKp/cNfyT4h+YiaUx7DMrTYXcLfpEVwu40fqiqmHb

s42RJ/yVMq4MKYEp0AvZcC8l/ByYvU9b/ogEKI8g175RLgVVmJqSaZW/w/ZhzG7u

89q1F1bYgJlEbrINSoBKC7CPyKB8N3KqTl1vOqiqSe6DSCzLIDk+NPEPSWGf3LoO

bAKcV9O2ml74rCipBBGyslsQVIINLxyUpXFC42/sS1ZN+MXYnQ==

\---- END SSH2 PUBLIC KEY ----

If you copy the public key from the saved file rather than from the PuTTYGen window in step 4 of the **Create an SSH key pair** section, remove the BEGIN and END lines, the Comment: line(s) and any carriage return, new line or line feed characters. The correct format should look like this:

ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAgXp4D3V6OGVv24Anh2P4Uh1N1KZ+DP9oT3sxE8U9MybSho1ev4eZuwso2q3M0tC1YU+PQu1RFd0hzZdcS8zTg7+soopI9HRaOoSLp5IyywDC28AvoJE8q9DtKZoKKp/cNfyT4h+YiaUx7DMrTYXcLfpEVwu40fqiqmHbs42RJ/yVMq4MKYEp0AvZcC8l/ByYvU9b/ogEKI8g175RLgVVmJqSaZW/w/ZhzG7u89q1F1bYgJlEbrINSoBKC7CPyKB8N3KqTl1vOqiqSe6DSCzLIDk+NPEPSWGf3LoObAKcV9O2ml74rCipBBGyslsQVIINLxyUpXFC42/sS1ZN+MXYnQ== An RSA SSH key example

If attempts are failing despite following these instructions, then copy the above example and attempt to add it. If the example key addition is successful, the failure is likely due to a carriage return, new line or line feed character that remains in the newly generated key.

The example key can be immediately deleted by clicking the button to the right of the key, in the listing of keys added to the Appliance.

Once a public key has been installed on the Appliance, follow the instructions below to configure PuTTY and log into the command line of the Appliance.

1.  1\.

    Run the PuTTY program (putty.exe).
2.  2\.

    In the PuTTY Configuration window's **Category** section, open the **Connection > Data** panel.
3.  3\.

    Enter the username "thousandeyes" in the **Auto-login username** field.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-12eb5992c41e50762323fc858aa9ab548be7176d%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-7.png?alt=media)

1.  1\.

    In the PuTTY Configuration window's **Category** section, open the **Connection** > **SSH** > **Auth** panel.
2.  2\.

    Click **Browse** and navigate to the location selected in Step 5 of the **Create an SSH key pair** section above.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-17b0b25d1d94159325a4bee760262c23c1d270bb%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-8.png?alt=media)

1.  1\.

    In the PuTTY Configuration window's **Category** section, open the **Session** panel.
2.  2\.

    Enter the IP address or hostname of the Enterprise Agent in the **Host Name (or IP address)** field.
3.  3\.

    Enter a name for this PuTTY session in the **Saved Sessions** field.
4.  4\.

    Click **Save** to save the session for future uses.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-69095851da5fe422d94a7bb3ffb12ff86b3b8af0%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-9.png?alt=media)

1.  1\.

    Click **Open** to open the SSH connection to the Appliance's command line.
2.  2\.

    If a passphrase was created in Step 3 of the **Create an SSH key pair** section, provide the passphrase to the SSH key.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0b779066c3bd665449713d6b938b3a2f1c938ec2%2Fproduct-documentation\_enterprise-agents\_connecting-to-the-thousandeyes-virtual-appliance-using-ssh-windows-10.png?alt=media)

1.  1\.

    If the login is successful, the prompt "\[email protected]\_hostname:\~ appears, indicating the user is in the home directory of the "thousandeyes" user.
2.  2\.

    Now you're SSH'd in. Have fun!

**Connection problem symptoms when using PuTTY SSH client:**

* `Error: Server unexpectedly closed network connection` error message
* `fatal: no matching mac found:...` error message

**Solution:** Make sure that PuTTY is at the current version as these errors have been encountered when using older versions of PuTTY.
