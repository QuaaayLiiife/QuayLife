# Using the FTP Server View

When you create an FTP server test, you get access to the FTP Server view. The FTP Server view uses the

[ThousandEyes standard layout](broken-reference)

. This article highlights elements specific to the FTP Server view.

This example shows the result of an FTP server download test to server ftp.ripe.net.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f5009f275f6a8293abd7b6c3ae76a6680936ca60%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-1.png?alt=media)

The FTP Server test measures the following metrics:

* **Availability** - Percentage of time that the site is available, aggregated across all agents.
* **Response time** - Also known as time-to-first-byte, this is the time elapsed from the beginning of the request (before the DNS request) until the agent receives the first byte of the response from the server.
* **Throughput** - The wire size divided by the receive time, expressed in megabits per second (Mb/s).

The FTP Server view shows two different data views, depending on whether a specific agent is selected, and varies depending on which metric is selected. Details for each selected metric are shown below.

The availability for a given agent is 100% if the FTP reply code is either 2xx or the code specified in the **Desired Reply Code** setting, and 0% otherwise. The average availability can take any value from 0% to 100%.

* **Without a Location Selected**

The **Map** tab shows a breakdown by error type, and shows any active alerts.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-60caa0b84db5c0cf9afbcffef85ca3cca01cdd62%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-2.png?alt=media)

The **Map** tab shows the FTP reply code or similar status, along with a green or red square icon, and any active alerts.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-45db5629fff113fa84de249178d4ebfea93971e4%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-3.png?alt=media)

Definitions of the possible error types are in the table below:

| Error Type  | Error Definition                                                                                                                     |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| DNS         | Failure to resolve a domain name to one or more IP addresses using DNS                                                               |
| Connect     | Failure to complete a TCP 3-way handshake (SYN, SYN-ACK, ACK)                                                                        |
| Negotiation | Failure after connect, up to the time the upload/download/list command is issued (including login failure)                           |
| Transfer    | Failure during the upload/download/list command execution                                                                            |
| FTP         | Receiving an FTP reply code that is not 2XX (default), or not the desired FTP reply code configured in Advanced Settings of the test |
| Content     | (optional) Failure to match returned content to an expression in the **Verify Content** field                                        |

With or without an agent selected, the timeline displays a graph of average availability. With an agent selected, that agent's availability data is plotted in addition to the average availability. The following image shows the availability metric with the Johannesburg agent selected. The agent's data is plotted using a green line, whereas the average availability data is plotted as a solid green area. The data round selector, indicated with the inverted yellow triangle at the top of the selector, is placed on a data round where the Johannesburg agent has 100% availability but the average availability is 80% due to one of the other four agents failing to successfully download the target file.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6135d5d05301a6588bb32756ece32cc59761fbef%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-4.png?alt=media)

The **Table** tab shows information for each of agents used in the test. This includes agent name, date/time that the data was captured, target IP address, FTP error type, and error details (if applicable). In the following image, we see that the 80% average availability displayed in the previous image was due to the Maidenhead, UK agent reaching the test timeout before completing the download. When you select an agent, the agent's row is highlighted in the table. In the image below, the Johannesburg agent has been selected.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dfb47c99621c0d64f49d380c762892097aafd65f%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-5.png?alt=media)

Also known as time-to-first-byte, response time is the time elapsed from the beginning of the request (before the DNS request) until the client receives the first byte of the response from the server. The response time metric is accompanied by the individual timings that make up response time.

* **Without a Location Selected**

The **Map** tab shows the computed averages area, which contains the response time and throughput averages from all agents that completed the test, and a pie chart breaking down the response into DNS lookup, connect, negotiation, and wait times. If you hover over the chart slices, tooltips show the individual timing averages via tooltips.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7f8fd0eb36c812c80529e17ce910bad08f7ad473%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-6.png?alt=media)

The **Map** tab shows the computed averages area, which contains the response time and throughput from the selected agent if it has completed the test, and a pie chart breaking down the response into DNS lookup, connect, negotiation, and wait times. If you hover over the chart slices, tooltips show the individual timings.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-716bfa60c2008da6a81c44818965b5d65b0c8917%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-7.png?alt=media)

With or without an agent selected, the timeline displays a graph of average response time. With an agent selected, that agent's response time data is plotted in addition to the average response time. The following image shows the response time metric with the Bruges agent selected. The agent's data is plotted using a blue line, whereas the average response time data is plotted as a solid blue area.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-24764e437787325e7bddf1c108845b8d64716936%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-8.png?alt=media)

The **Table** tab shows information for each of agents used in the test. This includes agent name, date/time that the data was captured, total response time, and the components of response time: DNS time, connect time, SSL time and wait time. When you select an agent, the agent's row is highlighted in the table. In the image below, no agent has been selected.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4fd340a2ba09389d3aff5c0a051f4c02b105bf8f%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-9.png?alt=media)

Throughput is the total wire size divided by the receive time. The throughput metric is accompanied by the detailed component timings.

In order to calculate the throughput, **Receive Time** needs to be >= 1 ms.

* **Without a location selected**

The **Map** tab shows the computed averages area, which contains the response time and throughput averages from all agents that completed the test, and a pie chart breaking down the throughput into DNS lookup, connect, negotiation, wait, and transfer times. If you hover over the chart slices, tooltips show the individual timing averages.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fffe5577c96dbed8e0ba648be08d8f5616d72532%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-10.png?alt=media)

The **Map** tab shows the computed averages area, which contains the response time and throughput from the selected agent if it completed the test, and timing averages via tooltips.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-aedcaa9166d3ee6ce2582bc9b37ea5a671f0628b%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-11.png?alt=media)

With or without an agent selected, the timeline displays a graph of average throughput. With an agent selected, that agent's throughput data is plotted in addition to the average throughput. The following image shows the throughput metric with the Bruges agent selected. The agent's data is plotted using a blue line, whereas the average throughput data is plotted as a solid blue area.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a0b709b4b8fda2a0bf95ebca4c16b4cce8a41f9c%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-12.png?alt=media)

The **Table** tab shows information for each of agents used in the test. This includes agent name, date and time that the data was captured, total throughput, and the detailed timings: DNS time, connect time, Negotiation time, wait time, Transfer time and total time. When you select an agent, the agent's row is highlighted in the table. In the image below, the Bruges agent has been selected.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-be836660d0c05bf0868625dd814626d0b52b00a9%2Fproduct-documentation\_thousandeyes-basics\_using-the-ftp-server-view-13.png?alt=media)
