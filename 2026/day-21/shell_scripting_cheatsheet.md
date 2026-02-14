# 🐚 Shell Scripting Cheat Sheet – DevOps Quick Reference Guide  
### 📌 Built During My #90DaysOfDevOps Journey  

> A practical, job-ready quick reference for daily DevOps tasks.  
> Short explanations. Real examples. Copy-paste friendly.

---

# 📊 Quick Reference Table

| Topic | Key Syntax | Example |
|-------|------------|---------|
| Variable | VAR="value" | NAME="DevOps" |
| Argument | $1, $2 | ./script.sh arg1 |
| If | if [ condition ]; then | if [ -f file ]; then |
| For Loop | for i in list; do | for i in 1 2 3; do |
| Function | name() { ... } | greet() { echo "Hi"; } |
| Grep | grep pattern file | grep -i "error" log.txt |
| Awk | awk '{print $1}' file | awk -F: '{print $1}' /etc/passwd |
| Sed | sed 's/old/new/g' file | sed -i 's/foo/bar/g' config.txt |

---

# 🟢 Task 1: Basics

## 🔹 Shebang
Tells system which interpreter to use.

[#!/bin/bash]

---

## 🔹 Running a Script

[chmod +x script.sh] → Make executable  
[./script.sh] → Run directly  
[bash script.sh] → Run using bash  

---

## 🔹 Comments

[# This is a comment]

[echo "Hello"  # Inline comment]

---

## 🔹 Variables

[NAME="Devesh"]  
[echo $NAME]  
[echo "$NAME"]  
[echo '$NAME']

✔ Use double quotes to preserve spaces.

---

## 🔹 Reading User Input

[read -p "Enter your name: " USER]  
[echo "Welcome $USER"]

---

## 🔹 Command Line Arguments

[$0] → Script name  
[$1] → First argument  
[$#] → Number of arguments  
[$@] → All arguments  
[$?] → Last command exit status  

Example:

[echo "Script: $0"]  
[echo "First arg: $1"]

---

# 🟡 Task 2: Operators & Conditionals

## 🔹 String Comparisons

[if [ "$a" = "$b" ]; then]  
[if [ -z "$var" ]; then]  
[if [ -n "$var" ]; then]

---

## 🔹 Integer Comparisons

[-eq] Equal  
[-ne] Not equal  
[-lt] Less than  
[-gt] Greater than  
[-le] Less or equal  
[-ge] Greater or equal  

Example:

[if [ $num -gt 10 ]; then]

---

## 🔹 File Test Operators

[-f file] → Regular file  
[-d dir] → Directory  
[-e file] → Exists  
[-r file] → Readable  
[-w file] → Writable  
[-x file] → Executable  
[-s file] → Not empty  

---

## 🔹 If-Else Syntax

[if [ condition ]; then]  
[   echo "True"]  
[elif [ condition ]; then]  
[   echo "Else If"]  
[else]  
[   echo "False"]  
[fi]

---

## 🔹 Logical Operators

[command1 && command2]  
[command1 || command2]  
[! condition]

---

## 🔹 Case Statement

[case $var in]  
[   start) echo "Starting";;]  
[   stop) echo "Stopping";;]  
[   *) echo "Invalid";;]  
[esac]

---

# 🔵 Task 3: Loops

## 🔹 For Loop (List Based)

[for i in 1 2 3]  
[do]  
[  echo $i]  
[done]

---

## 🔹 C-Style For Loop

[for ((i=1;i<=5;i++))]  
[do]  
[  echo $i]  
[done]

---

## 🔹 While Loop

[while [ $count -lt 5 ]]  
[do]  
[  echo $count]  
[done]

---

## 🔹 Until Loop

[until [ $num -gt 5 ]]  
[do]  
[  echo $num]  
[done]

---

## 🔹 Loop Control

[break] → Exit loop  
[continue] → Skip iteration  

---

## 🔹 Loop Over Files

[for file in *.log]  
[do]  
[  echo $file]  
[done]

---

## 🔹 Loop Over Command Output

[ls | while read line]  
[do]  
[  echo $line]  
[done]

---

# 🟣 Task 4: Functions

## 🔹 Define Function

[greet() {]  
[  echo "Hello $1"]  
[}]

---

## 🔹 Call Function

[greet DevOps]

---

## 🔹 Passing Arguments

Inside function → [$1], [$2]

---

## 🔹 Return Values

[return 1] → Exit status  
[echo "value"] → Output value  

---

## 🔹 Local Variables

[local var="value"]

---

# 🟤 Task 5: Text Processing Commands

## 🔹 Grep

[grep "error" file.log]  
[-i] ignore case  
[-r] recursive  
[-c] count  
[-n] line number  
[-v] invert match  
[-E] extended regex  

---

## 🔹 Awk

[awk '{print $1}' file]  
[-F:] field separator  
[awk 'BEGIN {print "Start"}']  
[awk 'END {print "Done"}']

---

## 🔹 Sed

[sed 's/old/new/g' file]  
[sed -i 's/foo/bar/g' file]  
[sed '2d' file]

---

## 🔹 Cut

[cut -d: -f1 /etc/passwd]

---

## 🔹 Sort

[sort file]  
[sort -n file]  
[sort -r file]  
[sort -u file]

---

## 🔹 Uniq

[uniq file]  
[uniq -c file]

---

## 🔹 Tr

[tr 'a-z' 'A-Z']  
[tr -d ',']

---

## 🔹 Wc

[wc -l file]  
[wc -w file]  
[wc -c file]

---

## 🔹 Head / Tail

[head -n 10 file]  
[tail -n 20 file]  
[tail -f file.log]

---

# 🔴 Task 6: Useful Real-World One-Liners

✔ Delete files older than 7 days  
[find /path -type f -mtime +7 -delete]

✔ Count lines in all .log files  
[wc -l *.log]

✔ Replace string in multiple files  
[sed -i 's/old/new/g' *.conf]

✔ Check if service running  
[systemctl is-active nginx]

✔ Disk usage alert  
[df -h | awk '$5 > 80']

✔ Tail logs for errors in real-time  
[tail -f app.log | grep -i error]

---

# ⚫ Task 7: Error Handling & Debugging

## 🔹 Exit Codes

[echo $?]  
[exit 0] → Success  
[exit 1] → Failure  

---

## 🔹 Strict Mode

[set -e] → Exit on error  
[set -u] → Unset variable error  
[set -o pipefail] → Catch pipe errors  
[set -x] → Debug trace  

Best Practice:

[set -euo pipefail]

---

## 🔹 Trap

[trap 'echo "Cleaning up"; rm -f temp.txt' EXIT]

Runs cleanup before script exits.

---

# 🏁 Final Notes

✔ Keep scripts modular  
✔ Use strict mode in production  
✔ Log outputs properly  
✔ Always validate inputs  
✔ Write reusable functions  

---

## 🚀 Built As Part of My DevOps Practice

This cheat sheet summarizes everything from basics to real-world automation scripts like:

- Log rotation  
- Backup automation  
- Service monitoring  
- Disk usage alerts  
- Cron job scheduling  

---

**📌 Keep Learning. Keep Automating. Keep Shipping.**

#ShellScripting #DevOps #Linux #Automation #90DaysOfDevOps 
