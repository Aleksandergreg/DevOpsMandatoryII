### Summary

Dockerized Sinatra app stopped running after VM reboot

### Detailed Description

 On March 28th at 20:49, the VM hosting our Sinatra app rebooted (likely due to Azure maintenance or automatic updates). After reboot, the application was no longer running. Investigation showed that our Docker container was not configured to restart automatically.

### Impact

The application was unavailable to users until it was manually restarted. As we haven't setup monitoring either, this wasn't detected before one of the group members randomly tried to access the site the morning after.

### Suggested Remediation

We updated our `docker-compose.prod.yml` file to include `restart: unless-stopped`, ensuring that the container will automatically restart after system reboots or crashes. We also plan to implement basic uptime monitoring and alerts.

In the future we should implement monitoring of our service, so that we'll actually get notified if anything like this happens again.
