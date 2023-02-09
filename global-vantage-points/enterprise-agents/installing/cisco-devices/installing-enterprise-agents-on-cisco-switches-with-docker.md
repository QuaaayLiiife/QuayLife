# Installing Enterprise Agents on Cisco Switches with Docker

catalyst#show app-hosting detail appid thousandeyes\_enterprise\_agent

App id : thousandeyes\_enterprise\_agent

Name : ThousandEyes Enterprise Agent

Path : flash:thousandeyes-enterprise-agent-4.3.0.cisco.tar

Activated profile name : custom

\---------------------------------------------

serial/shell iox\_console\_shell serial0

serial/aux iox\_console\_aux serial1

serial/syslog iox\_syslog serial2

serial/trace iox\_trace serial3

\---------------------------------------

MAC address : 52:54:dd:d:38:3d

Network name : mgmt-bridge-v21

Entry-point : /sbin/my\_init

Run options in use : -e TEAGENT\_ACCOUNT\_TOKEN=TOKEN\_NOT\_SET

\--hostname=$(SYSTEM\_NAME) --cap-add=NET\_ADMIN --mount

type=tmpfs,destination=/var/log/agent,tmpfs-size=140m --mount

type=tmpfs,destination=/var/lib/te-agent/data,tmpfs-size=200m -v

$(APP\_DATA)/data:/var/lib/te-agent -e TEAGENT\_PROXY\_TYPE=DIRECT -e

TEAGENT\_PROXY\_LOCATION= -e TEAGENT\_PROXY\_USER= -e

TEAGENT\_PROXY\_AUTH\_TYPE= -e TEAGENT\_PROXY\_PASS= -e

TEAGENT\_PROXY\_BYPASS\_LIST= -e TEAGENT\_KDC\_USER= -e TEAGENT\_KDC\_PASS=

\-e TEAGENT\_KDC\_REALM= -e TEAGENT\_KDC\_HOST= -e TEAGENT\_KDC\_PORT=88 -e

TEAGENT\_KERBEROS\_WHITELIST= -e TEAGENT\_KERBEROS\_RDNS=1 -e PROXY\_APT=

\-e APT\_PROXY\_USER= -e APT\_PROXY\_PASS= -e APT\_PROXY\_LOCATION= -e

TEAGENT\_AUTO\_UPDATES=1 -e

TEAGENT\_ACCOUNT\_TOKEN=nfhjzm8e8ikg07d4n31wcsws9bakcloh --hostname

Package run options : -e TEAGENT\_ACCOUNT\_TOKEN=TOKEN\_NOT\_SET

\--hostname=$(SYSTEM\_NAME) --cap-add=NET\_ADMIN --mount

type=tmpfs,destination=/var/log/agent,tmpfs-size=140m --mount

type=tmpfs,destination=/var/lib/te-agent/data,tmpfs-size=200m -v

$(APP\_DATA)/data:/var/lib/te-agent -e TEAGENT\_PROXY\_TYPE=DIRECT -e

TEAGENT\_PROXY\_LOCATION= -e TEAGENT\_PROXY\_USER= -e

TEAGENT\_PROXY\_AUTH\_TYPE= -e TEAGENT\_PROXY\_PASS= -e

TEAGENT\_PROXY\_BYPASS\_LIST= -e TEAGENT\_KDC\_USER= -e TEAGENT\_KDC\_PASS=

\-e TEAGENT\_KDC\_REALM= -e TEAGENT\_KDC\_HOST= -e TEAGENT\_KDC\_PORT=88 -e

TEAGENT\_KERBEROS\_WHITELIST= -e TEAGENT\_KERBEROS\_RDNS=1 -e PROXY\_APT=

\-e APT\_PROXY\_USER= -e APT\_PROXY\_PASS= -e APT\_PROXY\_LOCATION= -e

Application health information
