# Reports Snapshot Message Indicates Widget Configuration Was Corrupted

As of 9/14/2016, we have fixed an issue that affected reports with configurations that used grouping selectors such as “Group By" with a setting of "All". The list of affected grouping selectors and their widget types:

| Selector | Found in These Widget Types                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------- |
| Group By | Time Series, Time Series Stacked Area Chart, Stacked Bar Chart, Grouped Bar Chart, Pie Chart, Box-and-Whiskers, Map |
| Columns  | Table, Multi-metric Table                                                                                           |
| X/Y-Axis | Grouped Bar Chart, Stacked Bar Chart                                                                                |

These reports behaved as though the value of the selector was "Tests" rather than "All". When using certain values of Measure, this issue caused the data returned to be incorrect, based on the way data was aggregated to optimize (minimize) data requests between front-end and back-end systems. The list of affected Measures:

If the report used the other Measures (Mean, Total, Maximum, Minimum), the report data was not affected by this issue. Additionally, if the report did use an affected Measure but the results were the same due to conditions such as having only one test as source, "Tests" is equivalent to "All" and the report data was not affected by this issue.

Reports are now displaying data correctly, but some report snapshots that were generated with the issue still contain incorrect data. To address this issue, ThousandEyes has created a warning displayed on already-existing report snapshots that display bad data. The following warning appears on your widget:

"This snapshot widget’s configuration was corrupted. The data displayed is not aggregated as originally specified."

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-428177ae36ec017a5c21b1aff0ab4ca54b26acc0%2Fproduct-documentation\_reports\_reports-snapshot-message-indicates-widget-configuration-was-corrupted-1.png?alt=media)

This indicates that the data was aggregated by "Test" rather than by "All" even though the report configuration used the latter setting.
