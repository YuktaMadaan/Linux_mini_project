# Linux_mini_project
#!/bin/bash
# Server Status Script

echo "---- Server Status Report ----"
echo "Date & Time: $(date)"
echo "-------------------------------"

# System Uptime and Load
echo "System Uptime and Load:"
uptime
echo "-------------------------------"

# CPU Usage
echo "CPU Usage:"
top -bn1 | grep "Cpu(s)" | \
sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | \
awk '{print 100 - $1"% CPU Usage"}'
echo "-------------------------------"

# Memory Usage
echo "Memory Usage:"
free -h | awk '/^Mem:/ {print "Used: "$3", Free: "$4}'
echo "-------------------------------"

# Disk Usage
echo "Disk Space Usage:"
df -h | awk '$NF=="/"{print "Disk Used: "$5" on "$1}'
echo "-------------------------------"

# Network Activity
echo "Network Activity:"
echo "Active Connections: $(netstat -tn | grep ESTABLISHED | wc -l)"
echo "-------------------------------"

# Users Logged In
echo "Logged In Users:"
who
echo "-------------------------------"

# Current Running Processes
echo "Top 5 Processes by CPU Usage:"
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -6
echo "-------------------------------"
