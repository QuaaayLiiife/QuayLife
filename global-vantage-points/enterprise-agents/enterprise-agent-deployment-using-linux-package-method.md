# Enterprise Agent Deployment Using Linux Package Method

$ ./install\_thousandeyes.sh --help

Usage: ./install\_thousandeyes.sh \[-b \[-L] \[-W]] \[-f] \[-h] \[-I INSTALL\_LOG] \[-l LOG\_PATH] \[-t PROXY\_TYPE -P PROXY\_LOCATION \[-U PROXY\_USER -u PROXY\_PASS]] \[-r REPO] \[-s] \[-v AGENT\_VERSION] \[-O] ACCOUNT\_TOKEN

\-b Also install BrowserBot, an agent component that collects

Page Load and Transaction test data using an instance

\-L Also install international language packages for BrowserBot (requires -b)

\-W Install BrowserBot without its recommended packages (e.g. te-xvfb) (requires -b)

\-I \<INSTALL\_LOG> Set the install log location to INSTALL\_LOG

\-l \<LOG\_PATH> Set the log path to LOG\_PATH

\-t \<PROXY\_TYPE> Set the proxy type: DIRECT (default, no proxy), STATIC, or PAC

\-P \<PROXY\_LOCATION> Set the proxy location, format depends on PROXY\_TYPE

PROXY\_LOCATION is an invalid option for DIRECT

host:port for hostname or IPv4 address

\[IPv6 IP]:port for IPv6 address

URL where PAC file can be found

\-U \<PROXY\_USER> Set the proxy user to PROXY\_USER

\-u \<PROXY\_PASS> Set the proxy password to PROXY\_PASS

\-a \<PROXY\_AUTH\_TYPE> Set the proxy authentication type: BASIC (default), NTLM

\-r \<REPO> Force the installer to install from REPO (overriding original ones)

\-s Skip the repository creation

\-v \<AGENT\_VERSION> Specify agent version

\-O Install the agent, but do not start the agent services
