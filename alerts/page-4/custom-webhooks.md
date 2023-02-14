# Custom Webhooks

To create a new webhook, do the following:

1.  1\.

    In the ThousandEyes platform, go to **Alerts > Integrations**.
2.  3\.

    In the **Add New Custom Integration** panel, configure the fields for your new custom webhook:

| **Field**                 | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Name**                  | <p>A name for your custom webhook.</p><p>We recommend you use a human-readable, meaningful string. If you create multiple webhooks, it’s a good practice to use a consistent naming convention.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **URL**                   | <p>The target URL of the server associated with your webhook.</p><p><strong>Note</strong>: HTTP redirects are not accepted. Make sure you provide the final URL in this field.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Preset Configurations** | <p>These optional preset configurations provide a starting place from which you can create your custom webhook. If you use a preset configuration, it populates the fields below with sample content that you can adapt.</p><p><strong>Note</strong>: These preset configurations can serve as a guide, but you should verify that the resulting webhook’s structure and variables meet your requirements.</p><p>You can use any of the following preset configurations for your webhook:</p><ul><li>Generic</li><li>AppDynamics</li><li>Cisco Webex</li><li>Microsoft Teams</li><li>Slack</li><li>Splunk</li><li>[additional preset configurations to come]</li></ul><p><strong>Caution</strong>: When you select a preset configuration, any settings you have already made in the fields below are deleted.</p>                                                                  |
| **Auth Type**             | <p>Set the authentication method for your webhook:</p><ul><li>None</li><li>Basic</li><li>Token</li><li>OAuth</li></ul><p>For basic and token authentication, see</p><p><a href="../../.gitbook/assets/using webhooks server sample code included">Webhook Authentication</a></p><p>.</p><p>For OAuth, see</p><p><a href="../../.gitbook/assets/oauth">Using OAuth Authentication for Your Custom Webhook</a></p><p>.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **Header**                | <p>The <strong>Header</strong> field contains key/value pairs that make up the webhook’s HTTP header to a server and that function as metadata for the webhook.</p><p>The key/value pairs you enter here can be <em>static</em> (a set key and its set value) or <em>dynamic</em> (a set key and a variable as its value)</p><p>To add additional key/value pairs to the header of your webhook, click <strong>+ Key-Value Pair</strong> and enter the key and value.</p><p>To remove a key/value pair, click the <strong>-</strong> symbol.</p>                                                                                                                                                                                                                                                                                                                                    |
| **URL Query Parameter**   | <p>These parameters are appended to a URL to define content or actions, especially when integrating into a third-party system.</p><p>For guidance on defining query parameters, see</p><p><a href="https://handlebarsjs.com/guide/">Introduction to Handlebars</a></p><p>.</p><p>You can type directly into the text box to add URL query parameters to your webhook.</p><p>To see an expanded view of the contents of the field, click the arrows button.</p>                                                                                                                                                                                                                                                                                                                                                                                                                      |
| **Body**                  | <p>Define the body of your webhook to suit your needs. Note that the body</p><ul><li>Must be valid JSON.</li><li>Can include static or dynamic key/value pairs. Variables must match Handlebars syntax.</li></ul><p>You can type directly into the text box to customize the body of your webhook.</p><p>To see an expanded view of the contents of the field, click the arrows button.</p><p>For guidance on the editor for the <strong>Body</strong> field, see</p><p><a href="broken-reference">Working in the Webhook Editor</a></p><p>.</p><p>For the most up-to-date list of the variables you can use in your custom webhook, use the</p><p><a href="https://developer.thousandeyes.com/v6/">ThousandEyes API</a></p><p>. For convenience, the variables and some guidance on using them are available in</p><p><a href="broken-reference">Webhook Variables</a></p><p>.</p> |

1.  1\.

    \[Optional] Click **Test** to test your new custom webhook.
2.  2\.

    Your new webhook is listed on the **Integrations** screen.
3.  3\.

    \[Optional] Attach alert rules to your new webhook.

### Working in the Webhook Editor <a href="#working-in-the-webhook-editor" id="working-in-the-webhook-editor"></a>

#### Handlebars Templating Language <a href="#handlebars-templating-language" id="handlebars-templating-language"></a>

The ThousandEyes webhook templates use the Handlebars templating language. In fact, in a custom webhook, the **Body** field _is_ a Handlebars template.

When you write your own webhook, the syntax in the **Body** field must conform to the Handlebars syntax rules. For detailed information on the Handlebars language, see the

[Handlebars guide](https://handlebarsjs.com/guide/)

.

When you edit the **Headers**, **URL Query Parameters**, and **Body** fields, the webhook editor UI automatically suggests variables that match the text you have written or that was present in the template.

For example, if you type “a” into the editor, it suggests “alerts” as a possible completion. Once a given variable is completed, the editor suggests sub-variables available for it. For example, if the variable completed is “alert.”, the editor suggests all possible sub-variables, such as “id” “rule," and “firstSeen." You can prompt the editor's suggestions manually by typing **Ctrl+space**.

It’s a good practice to test your webhooks before deploying them. You can test a webhook

[while you are creating it](broken-reference)

, or after you have saved it:

1.  1\.

    In the ThousandEyes platform, go to **Alerts > Integrations**.
2.  2\.

    In the list of your integrations, find the webhook you want to test.

    The **Test Status** column shows whether the webhook has been tested.
3.  3\.

    Click the row for the webhook you want to test (or click its context menu and select **Edit**).
4.  4\.

    In the **Edit Custom Integration** panel, click **Test**.

    If your test fails, use the error message as displayed in this panel to troubleshoot your configuration.

When you click **Test**, the following elements of your webhook’s configuration are tested:

* The URL you have provided
* The authentication you have provided
*   The format of the payload

    The ThousandEyes platform sends a dummy HTTP alert trigger to test the format of the payload as defined in your webhook. It evaluates the server’s response to determine whether the server can accept the payload.

The **Test** function in this panel is not a foolproof verification of your webhook. The best way to test a webhook is with a real alert.

On the **Alerts > Integrations** screen, your webhooks are listed, showing their test status. The **Test Status** field can have the following values:

|   | This webhook has not been tested through the ThousandEyes platform.                                                                                                                                                                                                                                                                                                                                                                                              |
| - | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   | <p>This webhook has been tested through the ThousandEyes platform, but has failed this test.</p><p>If your webhook has a <strong>Failure</strong> status, it can still be attached to alert rules and might still be dispatched.</p><p>The Failure status typically means either that the server did not respond, or that the payload itself is malformed. However, in some cases these failures do not prevent the successful dispatch of a custom webhook.</p> |
|   | <p>This webhook has been tested through the ThousandEyes platform, and has successfully dispatched a test payload.</p><p>However, note that in some cases a successful test does not guarantee the successful dispatch of a custom webhook attached to an alert rule.</p>                                                                                                                                                                                        |

### Attaching Alert Rules to Your Webhook <a href="#attaching-alert-rules-to-your-webhook" id="attaching-alert-rules-to-your-webhook"></a>

1.  1\.

    In the ThousandEyes platform, go to **Alerts > Integrations**.
2.  2\.

    In the list of your integrations, find the webhook you want to attach alert rules to.
3.  3\.

    From its context menu, select **Manage Alert Rules**.
4.  4\.

    In the **Manage Alert Rules** panel, select the alert rule or rules that should be associated with this webhook.

    If you have a large number of alert rules, use the **Search** box to filter on a relevant string. You can also sort alert rules by name and by alert type.

You can attach any custom webhook to any Cloud and Enterprise Agent alert rule. However, some variables used in a webhook may not be applicable to some alert rules. In these cases, the inapplicable variable is passed as a null value to the system you have integrated with.

1.  1\.

    In the ThousandEyes platform, go to **Alerts > Integrations**.
2.  2\.

    In the list of integrations, find the webhook you want to edit.
3.  3\.

    Click the row for the webhook you want to edit (or click its context menu and select **Edit**).
4.  4\.

    In the **Edit Custom Integration** panel, make your changes.
5.  5\.

    \[Optional] Click **Test** to test your updated custom webhook.

### Duplicating an Existing Webhook <a href="#duplicating-an-existing-webhook" id="duplicating-an-existing-webhook"></a>

1.  1\.

    In the ThousandEyes platform, go to **Alerts > Integrations**.
2.  2\.

    In the list of integrations, find the webhook you want to duplicate.
3.  3\.

    From its context menu, select **Duplicate**.

    The system creates a new webhook that has

    * The name of the previous webhook, with the string _copy_ appended to it.
    * The same configuration as the previous webhook.
    * No alert rules attached to it.
4.  4\.

    \[Optional] Click **Test** to test your updated custom webhook.
5.  6\.

    \[Optional] Attach alert rules to your new webhook.
6.  1\.

    In the ThousandEyes platform, go to **Alerts > Integrations**.
7.  2\.

    In the list of integrations, select the webhook you want to delete.
8.  3\.

    From the context menu, select **Delete**.

Note: Deleting a webhook removes it from any alert rules that were attached to it. Deleted webhooks can be manually re-created, but cannot be restored.

### Troubleshooting Your Custom Webhook <a href="#troubleshooting-your-custom-webhook" id="troubleshooting-your-custom-webhook"></a>

If you’re encountering issues with your custom webhook, consider the following points:

*   A common way a webhook might fail despite passing testing is when conditional Handlebars helpers are used. For example, the template might contain a clause like the following:

    `"timeTriggered": {{#eq type 2 }} {{ alert.firstSeen.epochSecond }} {{/eq}}`

    If the underlying alert’s state is _triggered_, as it is in the sample we use when we test a webhook, this syntax renders correctly. But if the alert’s state is _cleared_, this syntax fails due to being invalid JSON: the **“timeTriggered”** key in the resulting object will have no value.
* Watch for illegal characters in the underlying alert data, particularly for custom headers. We apply URL escaping to query parameters, but not to the webhook's header or payload.
* Do not use **#** for custom helpers like **formatDate** or **formatExpression**.
