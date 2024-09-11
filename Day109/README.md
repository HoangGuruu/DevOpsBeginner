![Alt texts](../Images/p1.png)

# DevOps Beginner | Day 109 | Use EC2 Ubuntu Cron Job Automation 
Link Cron Sheet: https://crontab.guru/

```sh
crontab -e

* * * * * echo "Hello, World!" >> /backup/text.txt
```
```sh
# Create Service
nano /backup/my_script.sh
sudo chmod +x /backup/my_script.sh
```
# Backup Script Sample
```sh
#!/bin/bash

# Current time as a variable
TIME=`date +%b-%d-%y`
echo "time to backup $TIME" >> /home/ubuntu/backup/text.txt

# Filename
FILENAME=backup-$TIME.sql

# Backup directory
BACKUP_DIR=/backup

# Database credentials
DB_USER=your_username
DB_PASSWORD=your_password
DATABASE=your_database_name

# Command to backup database
# mysqldump --user=$DB_USER --password=$DB_PASSWORD $DATABASE > $BACKUP_DIR/$FILENAME
echo "dump database to folder backup" >> /home/ubuntu/backup/text.txt


echo "UPLOAD FILE BACKUP TO S3" >> /home/ubuntu/backup/text.txt

```

```sh
* * * * * /home/ubuntu/backup/backup_script.sh
```
```sh
tail -f /home/ubuntu/backup/text.txt
```
# Cron

```sh
# Basic Crontab Syntax
# * : Every value.
# */10 : Every 10 units (minutes, hours, etc.).
# 0 3 * * * : 3:00 AM every day.
# 0 0 1 * * : Midnight on the 1st of every month.
# 0 0 * * 0 : Midnight every Sunday.

* * * * * command to be executed
– – – – –
| | | | |
| | | | +—– day of week (0 – 6) (Sunday=0)
| | | +——- month (1 – 12)
| | +——— day of month (1 – 31)
| +———– hour (0 – 23)
+————- min (0 – 59)
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

# Create a servide : Tutorial Reference
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