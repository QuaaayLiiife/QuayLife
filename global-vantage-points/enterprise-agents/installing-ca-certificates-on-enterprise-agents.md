# Installing CA Certificates on Enterprise Agents

Enterprise Agents which perform Web Layer tests to targets protected by SSL/TLS (a target URL beginning with https://, ftps://, or ftp:// when using implicit-mode SSL/TLS) must validate the SSL server digital certificate and any intermediate certificates returned by the server or fetched by the client. Additionally, Enterprise Agents perform configuration download and data upload to ThousandEyes servers using TLS. Certificate validation requires that the sequence of certificates “chain” via digital signature back to the trusted root certification authority (CA) certificate that signed the previous certificate in the chain. As with most browsers and operating systems, ThousandEyes Enterprise Agents are pre-loaded with the standard X.509 CA certificate store of root CA certificates, which is provided by the

[Mozilla NSS project](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/)

.

In some environments, the certificate(s) returned by the server do not chain back to a CA certificate in the standard certificate store, causing Web Layer tests to produce certificate errors and/or the administrative communication to ThousandEyes to fail. To avoid the errors, customers can add any needed certificates to an Enterprise Agent’s certificate store. The steps to add certificates vary, depending on the type of Enterprise Agent.

Adding root CA certificates cannot be performed on Cloud Agents, due to the shared nature of Cloud Agents. Endpoint Agents are installed on standard operating systems which the customer controls, including control of the certificate stores.

### When to add certificates to an Enterprise Agent <a href="#when-to-add-certificates-to-an-enterprise-agent" id="when-to-add-certificates-to-an-enterprise-agent"></a>

When any Web Layer test (HTTP Server test, Page Load test, Transaction test or FTP Server test) or administrative communication from the Agent to ThousandEyes produces a certificate error, review the following scenarios to determine whether a root CA certificate must be added to the Enterprise Agent’s certificate store.

* **Certificates are issued by a private root CA certificate (internal PKI)**

Organizations which run their own public key infrastructure (PKI) will issue their own SSL server certificates, intermediate certificates (if any), and root CA certificate(s) which will not be included in the standard Mozilla root certificate store. The root CA certificate that issued certificates on servers that are the targets of ThousandEyes tests must be added to the Enterprise Agent.

If an Enterprise Agent is explicitly configured to use a proxy or if an Agent's web traffic is captured by a transparent proxy (a proxy that does not require configuration of the client) and the proxy performs SSL/TLS decryption, then the proxy's signing certificate(s) must be added to the Enterprise Agent. Proxy servers which decrypt and inspect data carried by SSL/TLS use a signing certificate to rewrite server certificates. Typically, the proxy signing certificate is not issued by one of the certificates in the standard certificate store. Often, the proxy software generates this certificate. The decrypting proxy scenario affects both ThousandEyes Web Layer tests and Agent communication to ThousandEyes.

*   **Self-signed SSL server certificate**

    A self-signed SSL server certificate will not chain back to a root CA certificate in the Enterprise Agent's standard certificate store. If correctly created, a self-signed certificate can be added to the Enterprise Agent's certificate store to eliminate certificate errors when the Agent performs tests to the server with the self-signed certificate.

    Additionally, if the target of the test does have certificates issued by a Certificate Authority whose root certificate is in the Agent's certificate store, but the target server does not return all needed intermediate certificates, and the customer cannot add the missing certificates on the server, then the intermediate certificate(s) can be added to the Enterprise Agent’s certificate store to create the “trust anchor” other than the root CA certificate. However, the customer should take great care in ensuring the veracity of any intermediate certificates, and understand and accept the impact the new trust anchor could have on other tests or aspects of the Agent operation, either in the present or in the future. ThousandEyes does not recommend adding intermediate certificates to an Enterprise Agent's certificate store.

### Converting certificates into PEM format <a href="#converting-certificates-into-pem-format" id="converting-certificates-into-pem-format"></a>

To add a CA certificate to an Enterprise Agent, the certificate file must be in

[PEM format](https://en.wikipedia.org/wiki/X.509#Certificate\_filename\_extensions)

. This format can easily be recognized by viewing the file:

\-----BEGIN CERTIFICATE-----

... (certificate content, base64 encoded)

\-----END CERTIFICATE-----

If your CA certificate is in a format other than PEM format, either use one of the free online certificate converters (

[link #1](https://www.sslshopper.com/ssl-converter.html)

,

[link #2](https://www.sslchecker.com/ssl\_converter)

or

[link #3](https://www.thesslstore.com/ssltools/ssl-converter.php)

), or use the commands below to convert your CA certificate into PEM format with the `openssl` command line utility.

Convert a DER file (.crt, .cer or .der) to PEM format:

openssl x509 -inform der -in infile -out outfile.pem

Convert a PKCS#12 file (.pfx or .p12) to PEM format:

openssl pkcs12 -in infile -out outfile.pem -nodes

### Installing on Virtual Appliances <a href="#installing-on-virtual-appliances" id="installing-on-virtual-appliances"></a>

Log into the Virtual Appliance's web management console, and click on the Network tab:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7ffefc45252baec4cb6964cb89dadac485adce95%2Fproduct-documentation\_enterprise-agents\_installing-ca-certificates-on-enterprise-agents-1.png?alt=media)

In the CA Certificate section, either paste the CA certificate into the **Add CA Certificate** field or browse to your PEM-formatted certificate file:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-77fee6be0421aee77801014803adda6a1ab14178%2Fproduct-documentation\_enterprise-agents\_installing-ca-certificates-on-enterprise-agents-2.png?alt=media)

If pasting, ensure that whole certificate is pasted into the field, including the "-----BEGIN CERTIFICATE-----" and "-----END CERTIFICATE-----" markers at the beginning and end of the certificate.

Multiple CA certificates may be installed by copying and pasting each certificate, concatenating the certificates in the **Add CA Certificate** field:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0221eb64f64b9a1ed1f0cad84cda50920158ee3e%2Fproduct-documentation\_enterprise-agents\_installing-ca-certificates-on-enterprise-agents-3.png?alt=media)

Click the **Save** button at the bottom of the page to complete the operation.

### Installing on supported Linux Distributions <a href="#installing-on-supported-linux-distributions" id="installing-on-supported-linux-distributions"></a>

When installing CA certificates on supported Linux distributions with the Enterprise Agent, CA certificates must be installed in two locations:

1.  1\.

    The system's CA certificate store
2.  2\.

    The NSSDB certificate store in the .pki/nssdb sub-directory of BrowserBot's home directory /var/lib/te-browserbot

    All commands should be executed as root. If logging into the system as a non-privileged user, begin each command with sudo.

The instructions below are provided in two sections for the two sets of supported Linux distributions: 1) Ubuntu and 2) Red Hat Enterprise Linux, CentOS and Oracle Linux. These instructions use the example certfile filename **MY-CA-CERT.pem**.

Install the required packages for managing CA certificates:

apt-get install ca-certificates libnss3-tools

Copy the certfile file (in PEM format; see above for conversion information) into the **/usr/share/ca-certificates** directory of the Enterprise Agent:

cp MY-CA-CERT.pem /usr/share/ca-certificates/

Open the **/etc/ca-certificates.conf** file in a text editor:

nano /etc/ca-certificates.conf

Append a line containing only the certfile filename to the end of the file:

\#...(existing certificates here)

Multiple certificate files can be added using multiple lines.

Update the system certificate store using the `update-ca-certificates` command, as shown below, with successful output:

Updating certificates in /etc/ssl/certs... 1 added, 0 removed; done.

Running hooks in /etc/ca-certificates/update.d...

Adding debian:MY-CA-CERT.pem

The system CA certificate store now contains your CA certificate(s).

For BrowserBot, first create the directory that will contain the certificate store:

mkdir -p /var/lib/te-browserbot/.pki/nssdb

Initialize the certificate store in directory created above:

certutil -N --empty-password -d sql:/var/lib/te-browserbot/.pki/nssdb

Add the CA certificate into the newly created certificate store:

\-d sql:/var/lib/te-browserbot/.pki/nssdb/ \\

\-i /usr/share/ca-certificates/MY-CA-CERT.pem

Change both the owner and the group of all newly created files and directories to browserbot:

chown -R browserbot.browserbot /var/lib/te-browserbot/.pki

Restart the te-browserbot service:

systemctl restart te-browserbot # Ubuntu 16.04

restart te-browserbot # Ubuntu 14.04

service te-browserbot restart # Ubuntu 16.04 and/or 14.04

#### Red Hat Enterprise Linux, CentOS and Oracle Linux <a href="#red-hat-enterprise-linux-centos-and-oracle-linux" id="red-hat-enterprise-linux-centos-and-oracle-linux"></a>

Install the required packages for managing CA certificates:

yum install ca-certificates nss-tools

Copy the certfile file (in PEM format; see above for conversion information) into the **/etc/pki/ca-trust/source/anchors/** directory of the Enterprise Agent:

cp MY-CA-CERT.pem /etc/pki/ca-trust/source/anchors/

Update the system certificate store using the **update-ca-trust** command:

The system CA certificate store now contains your the CA certificate.

For BrowserBot, first create the directory that will contain the certificate store:

mkdir -p /var/lib/te-browserbot/.pki/nssdb

Initialize the certificate store in the directory:

certutil -N --empty-password -d sql:/var/lib/te-browserbot/.pki/nssdb

Add the CA certificate to the newly created certificate store:

\-d sql:/var/lib/te-browserbot/.pki/nssdb/ \\

\-i /etc/pki/ca-trust/source/anchors/MY-CA-CERT.pem

On RHEL/CentOS 7 only, change both the owner and the group of all newly created files and directories to browserbot. On RHEL/CentOS 6 this step must be skipped:

chown -R browserbot.browserbot /var/lib/te-browserbot/.pki # RHEL / CentOS 7 only!

Restart the te-browserbot service:

systemctl restart te-browserbot # RHEL / CentOS 7

restart te-browserbot # RHEL / CentOS 6

The Enterprise Agent Docker image is based on Ubuntu. To install CA certificates on a Docker Enterprise Agent, follow the instructions for

[Installing on Ubuntu](https://docs.thousandeyes.com/product-documentation/enterprise-agents/installing-ca-certificates-on-enterprise-agents)

.

**IMPORTANT: If you replace the Enterprise Agent container, CA certificates will need to be reinstalled in the system store.**

Docker-based Enterprise Agents can be quickly reinstalled by removing the existing container with the `docker rm` command and redeploying the container by running the same `docker run` command that was used for initial container creation. Provided that the directories on the host created with the `-v` or `--volume` flag from the `docker run` command are not removed after `docker rm` is executed, and that those state directories are reused during the second `docker run` command execution, the replacement Enterprise Agent will retain the identity and general configuration of the previous container. However, replacing the container in this manner will not retain your CA certificates in the system store. The certificates will need to be reinstalled for the system store using the process described in the

[Installing on Ubuntu](https://docs.thousandeyes.com/product-documentation/enterprise-agents/installing-ca-certificates-on-enterprise-agents#ubuntu)

section. The certificates installed for the NSSDB/BrowserBot store will be retained, so customers do not need to re-add the certificate(s) to the NSSDB certificate store.

### Installing on Cisco Docker Devices <a href="#installing-on-cisco-docker-devices" id="installing-on-cisco-docker-devices"></a>

To install a CA certificate on a Cisco Docker Device:

1.  1\.

    Ensure your Docker configuration includes the SSL decrypting proxy location before running the Docker:

    Device(config)# app-hosting appid cat9kproxy

    Device(config-app-hosting)# app-resource docker

    Device(config-app-hosting-docker)# prepend-pkg-opts

    Device(config-app-hosting-docker)# run-opts 1 "-e TEAGENT\_ACCOUNT\_TOKEN"

    Device(config-app-hosting-docker)# run-opts 2 "--hostname DESIRED\_AGENT\_HOSTNAME"

    Device(config-app-hosting-docker)# run-opts 3 "-e TEAGENT\_PROXY\_TYPE=STATIC"

    Device(config-app-hosting-docker)# run-opts 4 "-e TEAGENT\_PROXY\_LOCATION=ssl-decrypting-proxy:3128"

    Device(config-app-hosting-docker)# exit

    Device(config-app-hosting)# exit
2.  2\.

    Launch the app and connect to the container shell

    For Cisco App-Hosting Docker Agents:

    \#app-hosting activate appid cat9kproxy

    \#app-hosting start appid cat9kproxy

    \#app-hosting connect appid cat9kproxy session
3.  3\.

    Confirm that the agent registration fails due to the proxy requiring a CA certificate in the agent logs:

    \# tail /var/log/agent/te-agent.log

    2022-06-30 03:35:52.211 INFO \[9997ff00] \[te.agent.ClusterMasterAdapter] {} Attempting to get agent id from https://sc1.thousandeyes.com

    2022-06-30 03:35:52.242 ERROR \[9997ff00] \[te.agent.status] {} Error calling createAgent: Curl error - Peer certificate cannot be authenticated with given CA certificates
4.  4\.

    Create a CA certificate file in **/usr/share/ca-certificates**, and copy/paste the PEM file content manually. The example below uses the text editor vi:

    \# vi /usr/share/ca-certificates/MY-CA-CERT.pem

    \-----BEGIN CERTIFICATE-----

    \-----END CERTIFICATE-----
5.  5\.

    Append the name of the created CA certificates file in **/etc/ca-certificates.conf**:

    \# vi /etc/ca-certificates.conf

    thousandeyes/Microsoft\_Root\_Certificate\_Authority\_2011.crt
6.  6\.

    Execute the command **update-ca-certificates** and wait for a successful output:

    Updating certificates in /etc/ssl/certs…

    1 added, 0 removed; done.

    Running hooks in /etc/ca-certificates/update.d…
7.  7\.

    Uninstall the **cisco-core-trsb** service. This step is only required for Cisco Agents:

    \# apt remove --purge cisco-core-trsb
8.  8\.

    Restart the te-agent service:

    Run: te-agent: 1s, normally up, want up
9.  9\.

    Check the agent log and make sure the previous curl error from step 2 disappears. If it no longer appears, the CA certificate has been installed correctly, and can now be imported to the new BrowserBot certificate store.
10. 10\.

    Install the **Certutil** tool:

apt-get install ca-certificates libnss3-tools

1.  1\.

    Create the directory that will contain the certificate store:

mkdir -p /var/lib/te-browserbot/.pki/nssdb

1.  1\.

    Initialize the certificate store in the new directory:

certutil -N --empty-password -d sql:/var/lib/te-browserbot/.pki/nssdb

1.  1\.

    Add the CA certificate into the newly created certificate store:

\-d sql:/var/lib/te-browserbot/.pki/nssdb/ \\

\-i /usr/share/ca-certificates/MY-CA-CERT.pem

1.  1\.

    Change both the owner and group of all newly created files and directories to browserbot:

chown -R browserbot.browserbot /var/lib/te-browserbot/.pki

1.  1\.

    Restart the te-browserbot service:
