

## Alert Manager
**Alert Manager** is a configurable tool that allows you to forward Verity *alarm* data to third-party messaging services such as email, PagerDuty, Microsoft Teams, and others.

The following diagram represents the relationship between Verity Alarm Manager, Alert Manager, and an arbitrary collection of connected messaging services.

![](media/889fd221544101b453bac1d7c2d01a7d.png)



# Process

The process for editing AlertManager is:

1. Edit ```/be_monitoring/alertmanager/user-config.yml``` (email/receiver settings)
2. Run ```/be_monitoring/utilities/render_alertmanager_config.sh``` to apply

Example: Email notifications via SMTP

```
#@data/values
---
smtp:
  smarthost: "smtp.company.com:587"
  from_address: "verity-alerts@company.com"
  auth_username: "verity-alerts@company.com"
  auth_password: "s3cretP@ss"
  require_tls: true

notification_email:
  to: "noc-team@company.com"
  send_resolved: true

```

**Example: Adding a Slack integration**

```
notification_receiver_integrations:
  webhook_configs:
    - url: "https://my-ticketing-system.com/api/alert"
      send_resolved: true
```

**Example: Adding a fully custom receiver + route**

```
additional_receivers:
  - name: critical-pagerduty
    pagerduty_configs:
      - service_key: "abc123"
        send_resolved: true

additional_routes:
  - matchers:
      - severity="critical"
    receiver: critical-pagerduty
    continue: false

```

Applying changes

```
run /be_monitoring/utilities/render_alertmanager_config.sh
```

This:

1. Merges vendor config + user values + overlay via ```ytt```
2. Writes the final alertmanager.yml
3. Reloads Alertmanager via ```POST /-/reload```
4. Persists user configs to ```/be_install/archive/``` for upgrade survival



