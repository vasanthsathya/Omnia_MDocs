---
hide:
- toc
---

# Whisper To Prometheus Metric Data Migration

The purpose of this service is to migrate from the legacy
metric time-series data format (Whisper) to the
current time-series data format (Prometheus).


The process involves running the script  **metric-migration.sh**, which may take several days to complete. This is because only up to one year's worth of data can be processed per metric for each device, and each device may have over 1,500 metrics.
Here are the steps the script performs to ensure a safe migration:

1. Creates the whisper migration files  
2. Performs a backup of the current Prometheus volume  
3. Creates the Prometheus migration files  
   and update Prometheus time-series (TSDB) database with migrated Whisper data  
4. Restarts the Prometheus container  
5. Verifies Prometheus is running and the migration was successful  
6. Shuts down the Whisper-Prometheus migration container


!!!Notice  "Notice: Use Screen"
    Due to the time this script will take to complete, you must start a **Screen** session before running the **metric-migration.sh** script. **Screen** is a Linux program that allows you to perform long-running background tasks on remote machines. It automatically resumes if the connection drops, making it ideal for the migration process. For more information about managing a **Screen** session, refer to: https://www.howtogeek.com/662422/how-to-use-linuxs-screen-command/"

## Performing the Migration:
Before following these instructions and running the **metric-migration.sh** script, you must allow the system to collect at least one day's worth of new metrics.


1. Login to the Monitoring VM via the **Verity Tunnel** by going to **Admin > VNFs > VNC Commander > Monitoring** and clicking on tunnel icon. 
![](media/monitoring_tunnel_diagram.png){:class="pop"}

1. In the **tunnel**, log in with the following credentials:
    - **Username**: verity
    - **Password**: *Your system Password*
1. Start a **Screen** session named ***whisper*** by running the following command:
    <code> /be_monitoring/whisper_data$ screen -S whisper </code>
1. Run the **metric-migration.sh** script
    <code> /be_monitoring/whisper_data$ sudo ./metric-migration.sh </code>
1. This will start the script, and the process may take several days to complete.

    !!!Notice " How to Detach From a  Screen Session" 
        You can detach from the **Screen** session using the hot-key combination: Ctrl+A, D (no visual indicator will show that you have clicked Ctrl+A, D the system will just return to the command prompt)

1. Check back in a few days to verify the migration was successful

    !!!Notice " How to Reattaching to a Screen Session" 
        If you  need to reattach to the **Screen** session, you run the following command:
            <code>/be_monitoring/whisper_data$ screen -r whisper </code>

1. If the migration is successful, terminate the **Screen** session by running the following command:
    <code> /be_monitoring/whisper_data$ screen -S whisper -X quit   </code>   

### Troubleshooting
If the migration was unsuccessful, perform the following steps:

1. Restart the prometheus container using the following command:
        <code> /be_monitoring$ sudo docker compose restart prometheus </code>
1. Restart the **metric-migration.sh** script 
        <code>/be_monitoring/whisper_data$ ./metric-migration.sh</code>            
        When you run the script, the migration will pick up where it left off if there is still data to migrate.
1. If you prefer to start the migration over, you can rerun the script using the following commands:            
        <code>/be_monitoring/whisper_data$ ./metric-migration.sh flush_setup_data </code>
        This will rerun the entire script again and may take several days to complete.
1. In the event that prometheus is no longer running as expected, the following set of commands can be used to restart the Prometheus environment. Be aware that this will **delete all previous container volumes and data**!

    - Shutdown the Monitoring Services
        1. <code> /be_monitoring$ sudo docker compose down </code>
        1. <code> /be_monitoring$ sudo docker volume rm be_monitoring_prometheus_data </code>
        1. <code> /be_monitoring$ sudo docker compose up -d </code>
        1. <code> /be_monitoring$ sudo ./whisper_data/reload_output.sh </code>

1. If you are unable to resolve the issue, please contact support for assistance.
        