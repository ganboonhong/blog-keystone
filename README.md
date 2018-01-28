# blog
keystone blog
db name: home

Start:
node keystone.js

Backup:
mongodump --db <yourdb> --gzip --archive=/path/to/archive

Restore:
mongorestore --gzip --db <yourdb> --archive=/path/to/archive

Cron job:
# backup on every Monday 00:00
0 0 * * 1 /home/francis/backup.sh

Backup Script:
timestamp=$(date +"%Y%m%d%H%M")
filename='home'
filename="$filename$timestamp.bak.gz"
mongodump --db home --gzip --archive=/home/francis/backup/$filename