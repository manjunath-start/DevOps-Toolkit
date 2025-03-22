# Validator Node Automation

Managing and maintaining validator nodes for blockchain networks requires automation to ensure uptime, reliability, and efficiency. This guide outlines essential automation tasks and how to implement them using **Cron Jobs** and **Systemd Timers**.

## 🚀 Automation Tasks

| Task | Description |
|------|------------|
| ✅ Restarting the validator node | Ensures the node runs continuously by restarting if it crashes. |
| ✅ Monitoring node health | Logs uptime and checks if the node is operational. |
| ✅ Rotating logs | Prevents disk space issues caused by excessive log storage. |
| ✅ Backing up blockchain data | Regular backups ensure data integrity and quick recovery. |
| ✅ Running maintenance scripts | Scheduled maintenance tasks improve node performance. |

## 🛠 Automation Methods

| Method | Description |
|--------|------------|
| 🕒 **Cron Jobs** | Time-based job scheduler to run scripts at specific intervals. |
| ⚡ **Systemd Timers** | More robust event-driven scheduling for automation. |

---

## ⏳ Automating Node Health Check & Restart

A common task is ensuring that the validator node remains active. If the node crashes, it must be restarted automatically.

### 📝 Step 1: Create the Health Check Script

Create a script file:
```bash
nano /home/user/node_health_check.sh
```

Paste the following script:
```bash
#!/bin/bash

# Check if the validator node is running
if ! pgrep -f "validator_node" > /dev/null; then
    echo "Validator node is down! Restarting..." | tee -a /var/log/node_monitor.log
    systemctl restart validator-node.service
else
    echo "Validator node is running." | tee -a /var/log/node_monitor.log
fi
```
Save and exit (**CTRL + X, then Y, then ENTER**).

### 🔑 Step 2: Make the Script Executable
```bash
chmod +x /home/user/node_health_check.sh
```

### 🕒 Step 3: Schedule a Cron Job
Open the crontab editor:
```bash
crontab -e
```

Add the following line at the end:
```bash
*/5 * * * * /home/user/node_health_check.sh
```

✅ This schedules the script to check the node every **5 minutes** and restart it if necessary.

Save and exit.

---

## ⚡ Alternative: Using Systemd Timers

Systemd Timers provide a more flexible alternative to Cron Jobs.

### 🔧 Step 1: Create a Systemd Service
Create a service file:
```bash
sudo nano /etc/systemd/system/node-health.service
```

Add the following content:
```ini
[Unit]
Description=Validator Node Health Check

[Service]
ExecStart=/home/user/node_health_check.sh
```
Save and exit.

### ⏳ Step 2: Create a Systemd Timer
Create a timer file:
```bash
sudo nano /etc/systemd/system/node-health.timer
```

Add the following content:
```ini
[Unit]
Description=Run Validator Node Health Check Every 5 Minutes

[Timer]
OnBootSec=5min
OnUnitActiveSec=5min
Unit=node-health.service

[Install]
WantedBy=timers.target
```
Save and exit.

### ▶️ Step 3: Enable and Start the Timer
```bash
sudo systemctl daemon-reload
sudo systemctl enable node-health.timer
sudo systemctl start node-health.timer
```

✅ The timer now runs every **5 minutes** to check and restart the node if needed.

---

## 📌 Conclusion

This guide helps automate validator node management using **Cron Jobs** or **Systemd Timers**. Implementing these methods ensures stability and reliability for your blockchain infrastructure.

🔹 **Cron Jobs** – Simple and effective for time-based scheduling.
🔹 **Systemd Timers** – More flexible and robust for automation.

🚀 Happy validating! 🎯
