# keystone blog

**DB**
---
db name: home

**Start:**

node keystone.js

**Backup:**
---
mongodump --db <yourdb> --gzip --archive=/path/to/archive
	
backup single collection:
mongodump --db=home --collection posts

copy to server:
scp -r dump/home/ francis@y-note.ddns.net:/home/francis/posts

**Restore:**
---
mongorestore --gzip --db <yourdb> --archive=/path/to/archive
		
if there's a memory restriction on digital ocean, instead of add SWAP, try to import collection one by one
mongorestore --db home --collection posts posts/posts.bson (copy the backup to local, then mongodump collection one by one)

**Cron job:**
---
(backup on every Monday 00:00)

0 0 * * 1 /home/francis/backup.sh

**Backup Script:**
---
timestamp=$(date +"%Y%m%d%H%M")

filename='home'

filename="$filename$timestamp.bak.gz"

mongodump --db home --gzip --archive=/home/francis/backup/$filename

