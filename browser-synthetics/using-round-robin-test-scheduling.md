# Using Round Robin Test Scheduling

When you configure a ThousandEyes test, the **Interval** setting controls the time between each test execution. Round-robin scheduling lets you stagger the execution of tests that are run at similar intervals.

Round-robin execution is limited to certain test types:

With Round-Robin an additional two settings, the **Schedule** mode and the **Subinterval**, are available to control the distribution of test execution, typically used when the test is assigned to multiple Cloud or Enterprise Agents.

When the Schedule mode is available, users may select either "Default" or "Round-robin" as the setting. In round-robin scheduling, each agent will be assigned a subinterval during which it must execute the test. Agents will be assigned to subintervals in a round-robin fashion.

This article explains the two scheduling modes, and provides a guide to using round-robin scheduling.

All ThousandEyes tests can be run in Default mode. The images below show the **Basic Configuration** tab of a test with the Schedule mode, when set to "Default", and a test without the Schedule mode (can only be run in Default scheduling mode).

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2b323888aa3424379f92a6520afb1cc9a0987f0f%2Fproduct-documentation\_tests\_using-round-robin-test-scheduling-1.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4a35c2a84def00346b5b5326c1f0e4aa56bec58f%2Fproduct-documentation\_tests\_using-round-robin-test-scheduling-2.png?alt=media)

In Default mode, a test can be executed by an agent at any time within the test's Interval setting. An agent will sequentially execute tests in a test queue. A given test will run whenever previous tests in the queue have completed. The start time for a given test within the test interval depends on the amount of other tests ahead in the queue, and the time taken by those tests to complete.

Currently, Browser-based tests (Page Load and Transaction test types) have a **Schedule** mode setting, and a **Subinterval** setting as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c2e97ebff3e70ac7e394cceb56ca710d3cac381f%2Fproduct-documentation\_tests\_using-round-robin-test-scheduling-3.png?alt=media)

In Round-robin mode, a test is executed by an agent based on the Subinterval setting. The test is assigned to agents' queues with a time-based offset from the beginning of the test round, to create subintervals. The offset varies by agent in order to evenly distribute all agents' test executions into subintervals over the time specified by the Interval setting.

* An agent may execute a test at any time within a subinterval
* The subinterval in which a particular agent executes a test cannot be configured
* For Page Load tests, the included HTTP Server test will be executed in the same subinterval as the Page Load test

The formulas below determine the number of subintervals and the number of agents in each subinterval. For the following settings

**I** = test **Interval** setting, in minutes **S** = test **Subinterval** setting, in minutes **A** = number of **Agents** assigned to the test

**N** = I ÷ S the number of subintervals in a test round

**X** = ⌈A ÷ N⌉ the maximum number of agents that will execute the test in a subinterval (the ⌈ ⌉ symbol indicates rounding up to the next integer)

If A ÷ N is not an integer, the remainder will be scheduled in a round-robin manner, i.e., one to the first subinterval, then one to the second, and so on, until all remaining agents are scheduled.

For the following settings:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-de43bca97e3922c0707a4431a2666d1ca9a03f1e%2Fproduct-documentation\_tests\_using-round-robin-test-scheduling-4.png?alt=media)

| Interval (I)                                           | 10 minutes |
| ------------------------------------------------------ | ---------- |
| Subinterval (S)                                        | 2 minutes  |
| Agents (A)                                             | 12         |
| Number of subintervals (N)                             | 5          |
| Maximum number of agents executing per subinterval (X) | 3          |

The execution of the test will be distributed as follows:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-436ae12c72d53b2fc77c588e61425a5d54b7f663%2Fproduct-documentation\_tests\_using-round-robin-test-scheduling-5.png?alt=media)

Round-robin scheduling can be useful when performing the same actions at the same time from multiple agents is not permitted. For example:

1.  1\.

    Steps in a Transaction test would produce conflicting results
2.  2\.

    Rate limits by a security device or security feature require even spacing of requests
3.  3\.

    Concurrent logins to a web application or proxy are not permitted

    To have exactly one agent per subinterval execute a test (**X** = 1) we can express the above equations as:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-382d624dc2770a318ec65c894559bd52b71af7a6%2Fproduct-documentation\_tests\_using-round-robin-test-scheduling-6.png?alt=media)

For example, with an interval time (**I**) of 15 minutes and a subinterval time (**S**) of 5 minutes, the test should have 3 agents assigned.

If fewer agents are assigned to the test than the number of subintervals, then for **A** agents, the test will be assigned to the first **A** subintervals.
