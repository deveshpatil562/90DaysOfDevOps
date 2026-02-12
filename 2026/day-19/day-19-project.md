# 🚀 Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab  
### #90DaysOfDevOps | Real-World Automation with Bash

---

## 📌 Day 19 Goal
Apply everything learned in **Days 16–18** by building **real-world shell scripting projects** used in production systems.

Today was all about **automation, maintenance, and scheduling**.

---

## 🧠 Tasks Overview

You will:
- Write a **log rotation script**
- Write a **server backup script**
- Schedule tasks using **crontab**
- Combine everything into a **maintenance automation script**

---

## 🧪 Task 1: Log Rotation Script

### 🎯 Objective
Create `log_rotate.sh` that:
- Accepts a log directory as an argument
- Compresses `.log` files older than **7 days**
- Deletes `.gz` files older than **30 days**
- Prints number of compressed & deleted files
- Exits with error if directory does not exist

---

### 📜 Script: `log_rotate.sh`

[
#!/bin/bash

LOG_DIR="$1"

if [ -z "$LOG_DIR" ]; then
  echo "Kindly provide Directory as an Argument:"
  echo "Usage: ./log_rotate.sh /path/to/logdir"
  exit 1
fi

if [ ! -d "$LOG_DIR" ]; then
  echo "Error: $LOG_DIR doesnt Exists!!"
  exit 1
fi

COMPRESSED=$(find "$LOG_DIR" -name "*.log" -mtime +7 -exec gzip {} \; | wc -l)
DELETED=$(find "$LOG_DIR" -name "*.gz" -mtime +30 -delete | wc -l)

echo "Compressed $COMPRESSED log files"
echo "Deleted $DELETED zip files"
]

---

### 🖥️ Sample Output (From My System)

[
[root@vbox scripts]# ./log_rotate.sh /var/log/devops
Compressed 4 log files
Deleted 4 zip files

[root@vbox scripts]# ./log_rotate.sh /var/log/teams
Error: /var/log/teams doesnt Exists!!

[root@vbox scripts]# ./log_rotate.sh
Kindly provide Directory as an Argument:
Usage: ./log_rotate.sh /path/to/logdir
]

<img width="613" height="168" alt="Screenshot 2026-02-12 140702" src="https://github.com/user-attachments/assets/623c479f-2f86-4496-b3c5-db73f5057e44" />
<img width="1177" height="736" alt="Screenshot 2026-02-12 140731" src="https://github.com/user-attachments/assets/4b8bf973-5a10-4d7d-bf99-73fcb38b5896" />


---

## 🧪 Task 2: Server Backup Script

### 🎯 Objective
Create `backup.sh` that:
- Takes **source directory** and **backup destination**
- Creates timestamped `.tar.gz` archive
- Verifies backup creation
- Shows archive name & size
- Deletes backups older than **14 days**
- Exits if source directory doesn't exist

---

### 📜 Script: `backup.sh`

[
#!/bin/bash

SRC="$1"
DEST="$2"
DATE=$(date +%Y-%m-%d)
ARCHIVE="backup-$DATE.tar.gz"

if [ ! -d "$SRC" ]; then
  echo "Source directory does not exist!"
  exit 1
fi

mkdir -p "$DEST"

tar -czf "$DEST/$ARCHIVE" "$SRC"

if [ $? -eq 0 ]; then
  echo "Backup created successfully:"
  ls -lh "$DEST/$ARCHIVE"
else
  echo "Backup failed!"
  exit 1
fi

find "$DEST" -name "backup-*.tar.gz" -mtime +14 -delete
]

<img width="762" height="815" alt="Screenshot 2026-02-12 153952" src="https://github.com/user-attachments/assets/b6c4cbc2-9321-47c2-bb27-a298152d0188" />
<img width="995" height="787" alt="Screenshot 2026-02-12 154024" src="https://github.com/user-attachments/assets/eff8a843-af71-4520-a903-bdfa288bfd93" />

---

## ⏰ Task 3: Crontab Scheduling

### 📖 Cron Syntax Reminder

<img width="347" height="212" alt="Screenshot 2026-02-12 195158" src="https://github.com/user-attachments/assets/8b04ecba-b9f7-4242-9dfd-7b7908a8cfab" />


---

### 🕒 Cron Entries (Not Applied — For Learning)

[
# Run log rotation daily at 2 AM
0 2 * * * /path/to/log_rotate.sh /var/log/devops

# Run backup every Sunday at 3 AM
0 3 * * 0 /path/to/backup.sh /data /backups

# Health check every 5 minutes
*/5 * * * * /path/to/health_check.sh
]

<img width="1167" height="647" alt="Screenshot 2026-02-12 192040" src="https://github.com/user-attachments/assets/4a255242-7f7a-4cd3-83d4-bd941cfb0656" />

---

## 🔧 Task 4: Scheduled Maintenance Script

### 🎯 Objective
Create `maintenance.sh` that:
- Calls log rotation
- Calls backup
- Logs everything with timestamps
- Writes output to `/var/log/maintenance.log`

---

### 📜 Script: `maintenance.sh`

[
#!/bin/bash

LOGFILE="/var/log/maintenance.log"

echo "$(date): Maintenance Started" >> "$LOGFILE"

./log_rotate.sh /var/log/devops >> "$LOGFILE" 2>&1
./backup.sh /data /backups >> "$LOGFILE" 2>&1

echo "$(date): Maintenance Completed" >> "$LOGFILE"
]

---

### ⏱️ Cron Entry for Maintenance Script

[
# Run maintenance daily at 1 AM
0 1 * * * /path/to/maintenance.sh
]

<img width="936" height="287" alt="Screenshot 2026-02-12 193834" src="https://github.com/user-attachments/assets/3b390f95-1b7d-4f12-b4a0-abbdc29bcf3f" />
<img width="807" height="648" alt="Screenshot 2026-02-12 193901" src="https://github.com/user-attachments/assets/dd137a54-70cf-4483-8861-140303022b54" />

---

## 📚 What I Learned (Key Takeaways)

1. **Functions & strict validation** make scripts production-ready  
2. **Cron + Bash** is a powerful combo for real server automation  
3. Logging with timestamps is critical for debugging & monitoring  

---

## ✅ Day 19 Completed!
From theory to **real-world automation** — this felt like actual **DevOps work** 🔥  
Onwards to the next challenge 🚀

