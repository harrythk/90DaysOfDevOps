## Script code:

#!/bin/bash

<<Notice

Usage: ./log_analyzer.sh <Log file path>
Notice


log_path=$1

if [ "$#" -eq 0 ]; then
        echo "Script usage: ./log_analyzer.sh <Log file path>"
        exit 1
fi

if [ -e "$log_path" ]; then
        echo "File exists"
else
        echo "File path doesn't exist"
fi

count_error() {

        count=$(grep "ERROR" "$log_path" | wc -l)
        echo "Total number of ERROR's $count"
}

critical_events() {
        echo "---- Critical Events ----"
        grep -n "CRITICAL" "$log_path"
}

top_error_message() {
        echo "----- Top 5 Error's -----"
        grep "ERROR" "$log_path" | awk '{$1=$2=$3=$4=$5=$6=""; print}' | sort | uniq -c | sort -rn | head -5
}

summary_report() {
        output_file=/home/ubuntu/devops/summary_reports/log_report_$(date +%Y-%m-%d).txt
        echo "Date of analysis: $(date +%Y-%m-%d)" >> "$output_file"
        echo "Analyzed log file: $log_path" >> "$output_file"
        total_lines=$(wc -l < "$log_path")
        echo "Total lines processed: $total_lines" >> "$output_file"
        total_error=$(count_error)
        echo "Total lines processed: $total_error" >> "$output_file"
        top_error_message >> "$output_file"
        critical_events >> "$output_file"

}

count_error
critical_events
top_error_message
summary_report

## OUTPUT

ubuntu@ip-172-31-18-78:~/devops$ ./log_analyzer.sh /home/ubuntu/app-logs/app.log
File exists
Total number of ERROR's 13
---- Critical Events ----
995:2015-07-29 19:29:23,859 - CRITICAL  [SendWorker:188978561024:QuorumCnxManager$SendWorker@679] - Interrupted while waiting for message on queue
----- Top 5 Error's -----
     12       Unexpected exception causing shutdown while sock still open
      1       Unexpected Exception:


## What commands/tools you used

grep
awk
sort
uniq -c
sort -rn
head -5

## What you learned (3 key points)
- print output of commands and funtions to a file
- count of number of lines
- Print a particular lines based on filter

