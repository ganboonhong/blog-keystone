# Package Manager
 [Unitech/pm2](https://github.com/Unitech/pm2)

**DB**
---
db name: home

**Start:**

```console
node keystone.js
```

**Backup:**
---
```console
mongodump --db <yourdb> --gzip --archive=/path/to/archive
```
	
backup single collection:
```console
mongodump --db=home --collection posts
```

copy to server:
```console
scp -r dump/home/ francis@y-note.ddns.net:/home/francis/posts
```

**Restore:**
---
```console
mongorestore --gzip --db <yourdb> --archive=/path/to/archive
```
		
If there's a memory restriction on digital ocean, instead of add SWAP, try to import collection one by one
mongorestore --db home --collection posts posts/posts.bson (copy the backup to local, then mongodump collection one by one)

**Cron job:**
---
```console
(backup on every Monday 00:00)

0 0 * * 1 /home/francis/backup.sh
```

**Backup Script:**
---
```console
timestamp=$(date +"%Y%m%d%H%M")

filename='home'

filename="$filename$timestamp.bak.gz"

mongodump --db home --gzip --archive=/home/francis/backup/$filename
```

**Allow script in Tiny-mce editor plugin**
---
1. Edit `blog/node_modules/keystone/admin/server/routes/index.js` line 50 on server (since node_moduels directory is ignored by git) by adding:
`additionalOptions: { extended_valid_elements : "script[src|async|defer|type|charset]" },`
2. comment the existing `additionalOptions` option

