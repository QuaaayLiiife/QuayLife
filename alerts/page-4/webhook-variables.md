# Webhook Variables

| **Variable**                                  | **Type**         | **Description**                                             |
| --------------------------------------------- | ---------------- | ----------------------------------------------------------- |
| `id`                                          | Numeric          | An identifier for the notification                          |
| `type.id`                                     | Numeric          | Clear (1) or Trigger (2)                                    |
| `alert.id`                                    | String           | An identifier for the alert                                 |
| `alert.severity.id`                           | String           | The severity of the alert                                   |
| `alert.firstSeen.epochSecond`                 | Date/time string | The time when the alert triggered                           |
| `alert.firstSeen.epochMilli`                  | Date/time string | The time when the alert triggered                           |
| `alert.timeCleared.epochSecond`               | Date/time string | The time when the alert cleared                             |
| `alert.timeCleared.epochMilli`                | Date/time string | The time when the alert cleared                             |
| `alert.rule.id`                               | Numeric          | An identifier for the alert rule                            |
| `alert.rule.name`                             | Numeric          | Name of the alert rule                                      |
| `alert.rule.account.id`                       | Numeric          | An identifier for the account that owns the alert rule      |
| `alert.rule.account.organization.id`          | Numeric          | An identifier for the organization that owns the alert rule |
| `alert.rule.account.organization.timezone.id` | String           | An identifier for the organization’s time zone              |
| `alert.rule.expression`                       | String           | The machine-readable alert rule expression                  |
| `alert.rule.notes`                            | String           | Alert rule notes                                            |
| `alert.rule.alertType.id`                     | String           | The alert rule’s alert type                                 |
