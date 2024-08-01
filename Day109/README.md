![Alt texts](../Images/p1.png)

# DevOps Beginner | Day 109 | Use EC2 Ubuntu Cron Job Automation 


```sh
crontab -e

# Create Service
sudo nano /usr/local/bin/my_script.sh

#!/bin/bash
echo "Hello, World!" >> /var/log/my_script.log

sudo chmod +x /usr/local/bin/my_script.sh
```

```bash
[Unit]
Description=My Custom Service
After=network.target

[Service]
ExecStart=/usr/local/bin/my_script.sh
Restart=always
User=ubuntu
Group=ubuntu

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl daemon-reload
sudo systemctl enable my_service.service
sudo systemctl start my_service.service

# Logs and Debugging
sudo journalctl -u my_service.service -f

watch -n 1 "ps aux | grep my_service"

```

# Cron

```sh
# Basic Crontab Syntax
# * : Every value.
# */10 : Every 10 units (minutes, hours, etc.).
# 0 3 * * * : 3:00 AM every day.
# 0 0 1 * * : Midnight on the 1st of every month.
# 0 0 * * 0 : Midnight every Sunday.
```
```sh
# list
crontab -l
# Edit cron jobs:
crontab -e
# Remove all cron jobs:
crontab -r
# View syslog for cron jobs:
grep CRON /var/log/syslog

tail -f /var/log/echo_hello.log

# Example Crontab Entries

# Run a script every 15 minutes:
*/15 * * * * /path/to/script.sh
# Run a script at 4:30 PM every Friday:
30 16 * * 5 /path/to/script.sh
# Run a script at midnight on the first day of every month:
0 0 1 * * /path/to/script.sh
```