# Optimizing SYN vs SACK Probing Methods to Avoid Unexplainable Packet Loss

When running Cloud and Enterprise Agent network tests through firewalls, a common issue is the “background noise” of packet loss between the agent and target without a clear cause.

An example of this is shown in the image below. There is a constant 4% packet loss, but none of the intermediate nodes in the path visualization show any packet loss that contributes to it. This article explains the cause and possible solutions for such noise.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ea4006fde790b439a6cd64b0fb5d60886043588b%2Fproduct\_documentation\_best\_practices\_Optimizing\_SYN\_vs\_SACK\_probing\_methods\_to\_avoid\_unexplainable\_packet\_loss1.png?alt=media)

Background Noise of Packet Loss

Two symptoms are clear indicators that the perceived packet loss is noise, rather than actual loss that should be investigated:

1.  1\.

    **The loss can’t be found in the path visualization**: If there is a node in the network causing the loss, you should investigate that first.
2.  2\.

    **The packet loss is constant**: In the example above we see that there is a constant 4% packet loss. In real life situations, this usually doesn’t happen; there are situations where a circuit consistently experiences loss, but usually not at such a constant rate.

If both symptoms are present, then the loss is likely background noise, and following the steps in this article will provide a good chance of solving the problem.

A network level test in ThousandEyes consists of two parts: An end-to-end measurement, which determines the packet loss and latency we see in the graph above, and the path trace, which builds the path visualization. For full details, see

[Network Tests Explained](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/network-tests/network-tests-explained)

.

The default method for end-to-end probing uses SACK-based measurement. This is the lightest-weight method on the network, the test target, and any firewalls in between.

Unfortunately, with some firewall settings, a false positive can cause some of the packets in the end-to-end measurements to be dropped, resulting in the background noise.

ThousandEyes recommends ensuring that your tests are as clean as possible when bringing them into production. This ensures that a real event is not missed because an operator thinks it's normal (for example, during implementation it might be known that the 4% loss is normal, but this kind of knowledge is easily lost).

SACK-based measurements are the default for a reason. So the first step is to try to resolve this issue without changing the probing method.

#### Check the Firewall Settings <a href="#check-the-firewall-settings" id="check-the-firewall-settings"></a>

The first thing to check is if there is a firewall within your control that is causing these issues. Work with your firewall administrator if there are any packet drops from or to the agent seeing this behavior, or if there is an advanced threat rule being triggered. Adjusting these firewall settings is the recommended solution.

However, if the solution can't be found by changing firewall settings, you can change the probing mechanism instead.

#### Change the Probing Mechanism <a href="#change-the-probing-mechanism" id="change-the-probing-mechanism"></a>

In normal circumstances this shouldn’t be an issue, but when there are resource constraint firewalls in between, or a large number of agents configured to run the same test, this might have adverse effects.

Always consider and test any impact this change might have on the rest of the environment before deploying in a production environment.

To change the probing mechanism, open the test configuration panel for the relevant test in the ThousandEyes web application, navigate to the **Network** section, and change the probing mode from **prefer SACK** (the default) to **Force SYN**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-46554aea571f5781ca5df50e54f71df6519f7d09%2Fproduct\_documentation\_best\_practices\_Optimizing\_SYN\_vs\_SACK\_probing\_methods\_to\_avoid\_unexplainable\_packet\_loss2.png?alt=media)

Save the changes, and observe the test to see if the background packet loss goes away.

Let's look again at the first test. In this instance, the firewall configuration couldn’t be changed, so instead we changed the probing mechanism to “Force SYN”.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d47719523fdb4ab8fc1070acfedf5c9d7c699b95%2Fproduct\_documentation\_best\_practices\_Optimizing\_SYN\_vs\_SACK\_probing\_methods\_to\_avoid\_unexplainable\_packet\_loss3.png?alt=media)

As you can see, the background noise is gone, and the only real packet loss is shown in the trace.
