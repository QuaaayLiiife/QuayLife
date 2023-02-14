# AppDynamics Integration

| **Name**                                         | Enter the name of your integration. This is a name for use within the ThousandEyes platform. Use a human-readable string that distinguishes this integration from any other integrations you may have configured.                                                                                                      |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **AppDynamics Instance**                         | Enter your specific AppDynamics instance in the form of `protocol://hostname:[port]`. For example, `https://www.te.appdynamics.com`. The ThousandEyes platform appends `/controller/rest/applications/%s/events` to the URL. If these values are included in what you enter here, the platform strips them.            |
| **Application Name**                             | Enter the specific AppDynamics application name. You can create multiple integrations that target different applications in the same instance.                                                                                                                                                                         |
| **Auth Type**                                    | <p>The AppDynamics integration supports Basic or OAuth. For more information on setting up OAuth, see</p><p><a href="../../.gitbook/assets/using webhooks server sample code included">Webhook Authentication</a></p><p>.</p>                                                                                          |
| **AppDynamics Username**                         | Use for Basic Authentication. Enter your AppDynamics username. Note: This username must be formatted as your AppDynamics \[email protected] without .com added. Additionally, the AppDynamics user must have the "Create Events" permission enabled under "Application Permissions" and "Roles" inside of AppDynamics. |
| **AppDynamics Password**                         | Use for Basic Authentication. Enter your AppDynamics password.                                                                                                                                                                                                                                                         |
| **Severity**                                     | Choose your desired AppDynamics severity for this alert: Info, Warning, or Error.                                                                                                                                                                                                                                      |
| **Tier**                                         | This is an optional field that matches a tier inside AppDynamics. If you use the **Tier** field, the value you enter here must match the tier listed in AppDynamics for the specified application.                                                                                                                     |
| **Node**                                         | This is an optional field that matches a node inside AppDynamics. If you use the **Node** field, the value you enter here must match the node listed in AppDynamics for the specified application.                                                                                                                     |
| **Business Transaction**                         | This is an optional field that matches a business transaction inside AppDynamics. If you use the **Business Transaction** field, the value you enter here must match the business transaction listed in AppDynamics for the specified application.                                                                     |
| **Learn more about the AppDynamics integration** | This link takes you to the documentation for the AppDynamics integration.                                                                                                                                                                                                                                              |
| **Cancel / Test / Add New Integration**          | Either cancel your integration; test your integration by sending a sample alert to your instance; or, once all fields are finalized, add the new integration you have just configured.                                                                                                                                 |