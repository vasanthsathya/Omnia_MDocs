# Alert Manager Setup

## Alarms

Alarms in Verity are error messages that notify you of changes within the network configuration. Alarms are listed in the **Alarms** window of the Verity App through the **Active Alarms** panel. 

When an alarm is triggered an alert notification payload is sent to the Alert Manager. Below is an example of what the alert notification payload contains. This information is used in the notifications sent out by the Alert Manager, which will be explained in more detail later.

![](media/alarm_payload.png)

## Alert Manager

**Alert Manager** is a configurable tool that allows you to forward Verity *alarm* data to third-party messaging tools such as email, PagerDuty, Microsoft Teams, and others.

The following diagram represents the relationship between Verity Alarm Manager, Alert Manager, and an arbitrary collection of connected messaging tools.

![](media/889fd221544101b453bac1d7c2d01a7d.png)

# Configuration

Integrating and configuring Alert Manager consists of these steps:

- Select the third party messaging solution (e.g., PagerDuty, Microsoft Teams) that you want to use and determine their compatibility for use in your system.
- Download the \`alertmanager.yml\` configuration file, edit it with the configuration details for your selection, and upload it to Verity. This file is in YAML format.
- Run terminal commands to update the system.

## Select Services

This is a partial example list of compatible services. For full list please see the [official documentation](https://prometheus.io/docs/alerting/latest/configuration/)

- Discord
- Email
- Slack
- WeChat
- Oauth2
- Microsoft Teams
- OpsGenie

## Alert Manager File

The bulk of your configuration is in the \`alertmanager.yml\` file. The default configuration that ships with \`alertmanager.yml\` is sufficient to get Alert Manager up and running. However, it does not include any integration points with notification services that are unique to your environment.

Configurations can be simple or complex depending on the number of notification services you integrate with. Click here to view the full configuration reference.

[Download Alert Manager YM Files (Blank and Example) ](downloads/alert_manager_files.zip)

### Conceptual Overview

Before editing the \`alertmanager.yml\` configuration file, it is important to understand how the code expressed in the file represents your system. This glossary serves that purpose.

**Receiver**

A Receiver is the configuration code needed to connect a Service. A properly configured system will always require at least one default Receiver.

**Notification**

Notifications are the messages that Receivers send to Services. Alarms are converted to Alerts and Alerts are converted into Notifications.

**Service**

A Service is a platform that receives Notifications. Common Services include email, Pager Duty and Microsoft Teams.

**Matchers**

Matchers are conditions that a Notification must meet.

**Routes**

Routes are conditional code that determines which Receiver a Notification is passed to. In code, Routes are composed of Matchers, Receivers, and other Routes.

### Alert Manager Rules

You conceptualize Alert Manager rules as routes and write rule sets to determine where notifications are sent. You must configure a default receiver for every notification, and you can set up additional services through child routes that match specific conditions.

In the simplified example below, alert data is routed to services based on matching criteria. Data matching ‘Emergency’ is sent to Pager Duty, data matching ‘All’ is sent to Email and data matching ‘Office’ is sent to Teams. All other data is routed through a default path and sent to a default service.

![](media/alert_manager_control_flow_diagram.png)

The \`alertmanager.yml\` file represents data as keys and values. Keys represent settings, and values are data assigned to them. We explain the example document section by section, describing the purpose of each key and value using bullet points.

![](media/example_alert_manager_file.png)

![](media/7b04b62137e7cfbda993ba90e4b68aed.png)

- **resolve_timeout**: Specifies the period after which an alert is considered resolved if it has not been updated.
- **smtp_smarthost**: Defines the address and port of the SMTP server (smarthost) used for sending emails. The port number is typically 25 for standard SMTP or 587 for SMTP over TLS (STARTTLS). This setting is essential for configuring the email notification system to relay messages through the specified SMTP server. **Example:** smtp.example.org:587
- **smtp_from**: Default SMTP From header field.
- **smtp_auth_username:** SMTP Auth email.
- **smtp_auth_password:** Application password from the email.

![](media/c5b98d0c3118b5aecb1919792283d501.png)

- **group_by**: Specifies a list of alert labels by which incoming alerts are grouped together.
- **group_wait:** Defines the initial waiting period before sending a notification for a group of alerts. Allows to wait for an inhibiting alert to arrive or collect more initial alerts for the same group. (Usually, \~0s to few minutes.)
- **group_interval:** Specifies the waiting period before sending a notification about new alerts that are added to an existing group of alerts for which an initial notification has already been sent.
- **repeat_interval:** Specifies the time to wait before resending a notification for an alert that has already been successfully sent. (Usually \~3h or more)
- **receiver:** Specifies the name of the default receiver to which all alerts will be sent.
- **routes:** Defines a set of instructions that determine where specific types of alerts should be sent. Each route includes matchers to filter alerts based on their labels and a designated receiver for alerts that meet the matching criteria.
    - **matchers:** A list of label-based filters that determine which alerts are matched by the route.
    - **receiver:** The name of the receiver that alerts matching the matchers will be sent to.

![](media/608f03f76642ffb561df046d03af1262.png)

- **inhibit_rules**: Defines rules that mute or suppress alerts (target) when another set of alerts (source) exists that matches a separate set of matchers. Both target and source alerts must have the same label values for the label names in the equal list.
    - **source_matchers:** A list of matchers that define the set of source alerts. If alerts match these criteria, they will trigger the inhibition rule.
        - **severity: critical** means that only alerts labeled as "critical" will trigger this inhibit rule.
    - **target_matchers:** A list of matchers that define the set of target alerts. These alerts will be muted when the matching source alerts are active.
        - **severity:** Defines the severity level of the target alerts that need to be matched for them to be muted. If the severity is set to **warning**, only alerts labeled with **severity: warning** will be muted by the inhibition rule.
    - **equal:** Defines a list of label names that must have identical values in both the source and target alerts for the inhibition rule to take effect.

![](media/7769bca7606d77314ca35e30cc9610c5.png)

- **receivers**: Specifies a list of named configurations for notification integrations. This example lists a Microsoft Teams receiver and an Email receiver. Detailed instructions for configuring your receivers are found in the [Receiver integration settings](https://prometheus.io/docs/alerting/latest/configuration/#receiver-integration-settings) documentation. The text \{\{.CommonLabels.\}\} and \{\{.CommonAnnotations.\}\} are used as variable placeholders for the data found in the alert notification payload sent by Verity.

![](media/b2409c2ad3bff086d849b83f991a6436.png)

## Final Steps

After you have finished customizing your alertmanager.yml configuration file, you must perform the following tasks:

1. Copy alertmanager.yml to the Verity Monitoring VM
2. Force reload of alertmanager.yml

### Copy alertmanager.yml to the Verity Monitoring VM

Use scp (secure copy) command to copy your alertmanager.yml file to the VM. Here is the syntax for a scp command:

<code> scp [source] [destination] </code>

If the VM IP was 10.1.10.6, the scp command would be this:

<code> scp alertmanger.yml user@10.1.10.6:/be_monitoring/alertmanager/ </code>

!!!notice "NOTE"

    The alertmanager.yml file must be copied into the /be_monitoring/alertmanager/ directory.

### Force reload of alertmanager.yml

Once the config file has been copied to the VM, run a curl command inside the VM to trigger an Alert Manager API call, which will reload the config file. To do so, go to *Admin/VNF/vNewtC Commander/Monitoring*. Click the tunnel button inside the Monitoring box. A window prompting you to open a remote tunnel appears. Open the tunnel.

![](media/monitoring_tunnel.png)

From the CLI, run:

<code> curl -X POST http://localhost:9093/-/reload </code>

To verify that the curl command was successful, run:

<code> echo $? </code>

If the return value is “0”, your Alert Manager is configured.