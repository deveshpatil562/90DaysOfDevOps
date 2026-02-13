# 🚀 Day 20 – Bash Scripting Challenge
## Log Analyzer and Report Generator

---

## 📌 Challenge Description

As a System Administrator, log files are generated daily across multiple servers.  
These logs contain important system events, warnings, failures, and critical errors.

The objective of this challenge is to build a Bash script:

log_analyzer.sh

This script automates:
- Log validation
- Error detection
- Critical event extraction
- Top error frequency analysis
- Report generation
- Optional log archiving

---

# 🎯 Expected Output

- Bash script: log_analyzer.sh
- Generated summary report: log_report_<date>.txt
- Documentation file: day-20-solution.md

---

# 🛠️ Solution Approach

---

## ✅ Task 1 – Input & Validation

The script:
- Accepts a log file path as a command-line argument
- Exits with an error if no argument is provided
- Exits with an error if file does not exist

Commands used:
[if [ $# -eq 0 ]]
[if [ ! -f "$1" ]]

---

## ✅ Task 2 – Error Count

Count total lines containing:
- ERROR
- Failed

Command used:
[grep -E -c "ERROR|Failed" "$logfile"]

---

## ✅ Task 3 – Critical Events

Search for lines containing CRITICAL and print them with line numbers.

Command used:
[grep -n "CRITICAL" "$logfile"]

Example Output:

--- Critical Events ---
Line 84: 2025-07-29 10:15:23 CRITICAL Disk space below threshold
Line 217: 2025-07-29 14:32:01 CRITICAL Database connection lost

---

## ✅ Task 4 – Top 5 Error Messages

Steps:
1. Extract lines containing ERROR
2. Remove timestamps
3. Count occurrences
4. Sort in descending order
5. Display top 5

Command pipeline used:

[grep "ERROR" "$logfile" | awk '{$1=$2=$3=""; print}' | sort | uniq -c | sort -rn | head -5]

---

## ✅ Task 5 – Summary Report Generation

Generate report file:

log_report_$(date +%Y-%m-%d).txt

Command used:
[date +%Y-%m-%d]

Report includes:
- Date of analysis
- Log file name
- Total lines processed
- Total error count
- Top 5 error messages
- Critical events

---

## ✅ Task 6 – Archive Processed Logs (Optional)

Features:
- Create archive/ directory if not exists
- Move processed log file to archive/
- Print confirmation message

Commands used:
[mkdir archive]
[mv "$logfile" archive/]

---

# 🧠 Full Script – log_analyzer.sh

[#!/bin/bash

# ------------------------------
# Log Analyzer & Report Generator
# ------------------------------

# Task 1: Input Validation
if [ $# -eq 0 ]; then
    echo "Error: No log file provided."
    exit 1
fi

logfile="$1"

if [ ! -f "$logfile" ]; then
    echo "Error: File does not exist."
    exit 1
fi

# Task 2: Count Errors
error_count=$(grep -E -c "ERROR|Failed" "$logfile")

echo "Total Errors: $error_count"

# Task 3: Critical Events
critical_events=$(grep -n "CRITICAL" "$logfile")

echo "--- Critical Events ---"
echo "$critical_events"

# Task 4: Top 5 Errors
top_errors=$(grep "ERROR" "$logfile" \
    | awk '{$1=$2=$3=""; print}' \
    | sort \
    | uniq -c \
    | sort -rn \
    | head -5)

echo "--- Top 5 Error Messages ---"
echo "$top_errors"

# Task 5: Generate Report
report="log_report_$(date +%Y-%m-%d).txt"

{
echo "Log Analysis Report"
echo "Date: $(date)"
echo "Log File: $logfile"
echo "Total Lines: $(wc -l < "$logfile")"
echo "Total Errors: $error_count"
echo ""
echo "--- Top 5 Errors ---"
echo "$top_errors"
echo ""
echo "--- Critical Events ---"
echo "$critical_events"
} > "$report"

echo "Report generated: $report"

# Task 6: Archive Log
archive_dir="archive"

if [ ! -d "$archive_dir" ]; then
    mkdir "$archive_dir"
fi

mv "$logfile" "$archive_dir/"

echo "Log file archived to $archive_dir/"
]

---

# 🖥️ Sample Execution

Command:
[./log_analyzer.sh sample_log.log]

Sample Console Output:

Total Errors: 129

--- Critical Events ---
Line 84: CRITICAL Disk space below threshold
Line 217: CRITICAL Database connection lost

--- Top 5 Error Messages ---
45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory

---

# 🔧 Tools & Commands Used

- grep
- awk
- sort
- uniq
- wc
- date
- mkdir
- mv
- Bash conditionals
- Command substitution using $()

---

# 📚 What I Learned

1. Log analysis becomes powerful when combining grep, awk, sort, and uniq in pipelines.
2. Input validation is critical in scripting to avoid runtime failures.
3. Automating report generation improves efficiency and reduces manual monitoring effort.

---

# ✅ Conclusion

This project demonstrates practical log parsing, text processing, automation, and report generation using Bash scripting — essential skills for Linux administrators and DevOps engineers.
