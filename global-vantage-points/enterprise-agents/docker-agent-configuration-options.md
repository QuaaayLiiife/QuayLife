# Docker Agent Configuration Options

Device(config)# app-hosting appid thousandeyes\_enterprise\_agent

Device(config-app-hosting)# app-resource docker

Device(config-app-hosting-docker)# prepend-pkg-opts

Device(config-app-hosting-docker)# run-opts 1 "-e TEAGENT\_ACCOUNT\_TOKEN"

Device(config-app-hosting-docker)# run-opts 2 "--hostname DESIRED\_AGENT\_HOSTNAME"

Device(config-app-hosting-docker)# run-opts 3 "-e TEAGENT\_PROXY\_TYPE=STATIC

Device(config-app-hosting-docker)# run-opts 4 "-e TEAGENT\_PROXY\_LOCATION=proxy.something.other:80"

Device(config-app-hosting-docker)# exit

Device(config-app-hosting)# exit
