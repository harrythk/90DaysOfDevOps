## Task 1: Log Rotation Script
Create log_rotate.sh that:

Takes a log directory as an argument (e.g., /var/log/myapp)
Compresses .log files older than 7 days using gzip
Deletes .gz files older than 30 days
Prints how many files were compressed and deleted
Exits with an error if the directory doesn't exist

==============================================================================================================================
#!/bin/bash

<<usage
./log_rotate.sh <log directory path>
usage

display_usage() {

        echo "Usage: ./log_rotate.sh <log directory path>"
}

if [ $# -eq 0 ]; then
        display_usage
        exit 1
fi

log_dir=$1

if [ ! -d "$log_dir" ]; then
        echo "Error: Directory does not exist."
        exit 2
fi

log_compress() {

        compress_count=$(find "$log_dir" -name "*.log" -mtime +7 | wc -l)
        echo "Number of files compressed: $compress_count"
        find "$log_dir" -name "*.log" -mtime +7 -exec gzip {} \;
}

delete_logs() {

        delete_count=$(find "$log_dir" -name "*.gz" -mtime +30 | wc -l)
        echo "Number of files deleted: $delete_count"
        find "$log_dir" -name "*.gz" -mtime +30 -exec rm {} \;
}

log_compress
delete_logs
==============================================================================================================================

## Task 2: Server Backup Script
Create backup.sh that:

Takes a source directory and backup destination as arguments
Creates a timestamped .tar.gz archive (e.g., backup-2026-02-08.tar.gz)
Verifies the archive was created successfully
Prints archive name and size
Deletes backups older than 14 days from the destination
Handles errors — exit if source doesn't exist

#!/bin/bash

<<Comment

Usage: backup.sh <source directory> <backup directory>

Comment

source_dir=$1
timestamp=$(date '+%Y-%m-%d-%H-%M-%S')
backup_dir=$2

compress_file() {
        tar -czf "${backup_dir}/backup_$timestamp.tar.gz" "${source_dir}"

        if [ $? -eq 0 ]; then
                echo "Backup file created sucessfully"
                echo "Archived file name: ${timestamp}.tar.gz"
                echo "Archive Size: $(du -h "${backup_dir}/backup_$timestamp.tar.gz")"
        fi
}

del_backup() {

        echo "Deleting files"
        bckup=($(ls -t "${backup_dir}/backup_"*.tar.gz))
        find "$backup_dir" -type f -mtime +14 -exec rm {} \;

}

compress_file
del_backup

==============================================================================================================================

## Task 3: Crontab

# Read: crontab -l — what's currently scheduled?

ubuntu@ip-172-31-18-78:~/devops$ crontab -l 
no crontab for ubuntu

# Write cron entries (in your markdown, don't apply if unsure) for:
Run log_rotate.sh every day at 2 AM
Run backup.sh every Sunday at 3 AM
Run a health check script every 5 minutes

0 2 * * * /home/ubuntu/devops/log_rotate.sh /var/log/myapp
0 3 * * * /home/ubuntu/devops/backup.s /home/ubuntu/devops /home/ubuntu/devops/test_backup_dir/

==============================================================================================================================

## Task 4: Combine — Scheduled Maintenance Script
Create maintenance.sh that:

Calls your log rotation function
Calls your backup function
Logs all output to /var/log/maintenance.log with timestamps
Write the cron entry to run it daily at 1 AM


#!/bin/bash

LOG_FILE="/var/log/maintenance.log"

source_dir="/home/ubuntu/devops"
backup_dir="/home/ubuntu/devops/test_backup_dir"
log_dir="/var/log/myapp"

source /home/ubuntu/devops/log_rotate.sh
source /home/ubuntu/devops/backup.sh

echo "$(date): running log compression..." >> "$LOG_FILE"
log_compress

echo "$(date): running log backup..." >> "$LOG_FILE"
compress_file

echo "$(date): Deleting old files..." >> "$LOG_FILE"
del_backup

==============================================================================================================================


