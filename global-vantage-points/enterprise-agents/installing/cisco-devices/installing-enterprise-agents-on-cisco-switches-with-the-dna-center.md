# Installing Enterprise Agents on Cisco Switches with the DNA Center

ThousandEyes Enterprise Agents can be installed on Cisco devices using the Cisco DNA Center. This article provides a video walkthrough of the installation and configuration process, as well as some troubleshooting solutions.

Before following the video instructions, users should have the following configured/set up:

* Login credentials to the DNA Center with either **Network Admin** or **Super Admin** permissions.
* A VLAN for the Enterprise Agent to use.
* An IP address with a routable subnet with permission to connect to the ThousandEyes cloud, allowing outgoing HTTPS connections directly or through a proxy server.
*

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-81ca7552bbb9ee7eb80689ca2e2d4a494f5fc571%2Finstall-enterprise-agent-with-dna-center\_1.png?alt=media)

#### Incorrect file download from Cisco DNA Center versions 2.2.2.x and 2.2.3.x <a href="#incorrect-file-download-from-cisco-dna-center-versions-2.2.2.x-and-2.2.3.x" id="incorrect-file-download-from-cisco-dna-center-versions-2.2.2.x-and-2.2.3.x"></a>

There is an existing bug with Cisco DNA Center versions 2.2.2.x and 2.2.3.x that causes an unsupported version of the ThousandEyes Enterprise Agent to be downloaded. The summary and workaround are listed below; more details can be found here:

[Cisco Issue Tracker](https://bst.cloudapps.cisco.com/bugsearch/bug/CSCwb74636)

.

When running Cisco DNA Center versions 2.2.2.x or 2.2.3.x, the hyperlink to download the **tar.gz** file automatically redirects to ThousandEyes Enterprise Agent version 4.2.2. This version is not supported on Cisco DNA Center versions earlier than 2.3.3.x, and will cause an error due to the changes in the **controller.yaml** file.

To workaround this issue, ThousandEyes Enterprise Agent version 4.1.0 can be downloaded and imported instead. This version is still supported under the correct schema:.

#### Deploy failed (ERR\_AH\_1000): 400 Client Error: Bad Request ("Duplicate mount point: /var/tmp/te-agent") <a href="#deploy-failed-err_ah_1000-400-client-error-bad-request-duplicate-mount-point-var-tmp-te-agent" id="deploy-failed-err_ah_1000-400-client-error-bad-request-duplicate-mount-point-var-tmp-te-agent"></a>

There is an existing bug that caused users trying to deploy the ThousandEyes Enterprise Agent with Cisco DNA Center 2.3.2.x to receive the failure message `Deploy failed (ERR_AH_1000): 400 Client Error: Bad Request ("Duplicate mount point: /var/tmp/te-agent")`. A workaround is listed below; more details can be found here:

[Cisco Issue Tracker](https://bst.cloudapps.cisco.com/bugsearch/bug/CSCvz84369)

.

Navigate to the ThousandEyes app in the Cisco DNA Center Application Hosting page. In the docker runtime options, remove the following line from the configuration:

`--mount type=tmpfs,destination=/var/tmp/te-agent,tmpfs-size=340m`

Save the changes, and the setup should then work as expected.
