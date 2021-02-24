# The password for portainer.db

After experimenting with Docker and Portainer for a while, a made some custom templates I wanted to copy from the old test server to the new production environment into a own template container for using them as a external templates source. 

So while researching where to find the data in my volume folder on the docker host, I found a database file "portainer.db". 

So I copied it with "scp" to my windows machine an opened it with "DB Browser for SQLite" which prompted me with a "SQLCiper encryption" dialog.

**TODO: Insert image**

So after doing some googling where to get this password, I recognized that the "portainer.db" is not even a SQLite database but a [BoltDB](https://github.com/boltdb) database file.

So after opening it with [boltbrowser](https://github.com/br0xen/boltbrowser) (now without password :), I found all my templates as JSON in the bolt database under the "templates" key, ready to copy them to my new custom templates.json.

**TODO: Insert image**
