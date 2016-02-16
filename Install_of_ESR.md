#How to Install the ESR patch

# How to use the ESR #
I publish this as a patch based on Percona-Server-5.5.15. I hope this can be merge into the main tree of Percona Server or MySQL Community Server ,so than i do not need maintain it at google code.

### For Percona-Server-5.5.15 ###
  * Download [Percona-Server-5.5.15-rel21.0.tar.gz](http://www.percona.com/downloads/Percona-Server-5.5/Percona-Server-5.5.15-21.0/source/)
  * Checkout the patch from google code: [Google Code SVN](http://code.google.com/p/enhanced-semi-sync-replication/source/checkout).
  * tar zxf Percona-Server-5.5.15-rel21.0.tar.gz
  * so:
```
$ls
Percona-Server-5.5.15-rel21.0 ESR.percona.5.5.15.patch
```
  * patch -p0 < ESR.percona.5.5.15.patch
  * patch -p0 < ESR.percona.5.5.15.fix-bug-44058.patch
  * Compile the Server: cmake . -DCMAKE\_INSTALL\_PREFIX=/opt/mysql  -DEXTRA\_CHARSETS=all && make -j 8 && make install ...
  * configure the semi-sync with **rpl\_semi\_sync\_master\_wait\_before\_commit=1** in my.cnf ,so something like this:
```
## semi-sync master ##
plugin_load=rpl_semi_sync_master=semisync_master.so
rpl_semi_sync_master_enabled=1
rpl_semi_sync_master_timeout=5000
rpl_semi_sync_master_trace_level=32
rpl_semi_sync_master_wait_before_commit=1

sync_binlog=1
```

### For MySQL Community Server 5.5.16 ###

it't the same as the Percona-Server. Of course, you should use [mysql-5.5.16.tar.gz](http://dev.mysql.com/downloads/mysql/) and ESR.MySQL.5.5.16.patch


# Details #

Add your content here.  Format your content with:
  * Text in **bold** or _italic_
  * Headings, paragraphs, and lists
  * Automatic links to other wiki pages