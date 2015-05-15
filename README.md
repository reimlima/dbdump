dbdump
--------------------------------------------------------------------------------

Backup and purge script for MySQL.


Notice
--------------------------------------------------------------------------------

This script was tested and work well in:

* Linux
	- OS Distribution: CentOS release 6.6 (Final)
	- Kernel: 2.6.32-504.3.3.el6.x86_64
	- GNU bash: version 4.1.2(1)-release (x86_64-redhat-linux-gnu)

Changelog
--------------------------------------------------------------------------------

2015-02-21	- v2	- First Stable Release.

2015-02-24	- v2.1	- Added "--single-transaction" parameter for "non lock" entire database.

2015-02-26	- v2.2	- Removed unnecessary lock file.
			- Better comment about conf file.

2015-05-15      - v2.3	- Added option to send dump file to a remote server via  rsync.

How to use it
--------------------------------------------------------------------------------

CONF FILE:

Just  fill  the  configuration  file  with  the  values  for DBUSER, DBPASSWORD,
DBARRAY, DUMPFILENAME, DUMPPATH, DUMPRETENTION, DBDUMPLOG, then run the script.

Legend:

	DBUSER:		MySQL Access Login
	
	DBPASSWORD: 	MySQL Access Password
	
	DBARRAY:	Databases to Backup
			fill it in format like => "db1 db2 dbN"
			Empty = "All Databases"
					
	DUMPFILENAME:	Name of Dump File
	
	DUMPPATH:	Path to dumpfile, no slash in the end
	
	DUMPRETENTION:	Time to retention in days,
			older files than "DUMPRETENTION" will be removed
					
	DBDUMPLOG:	Log File

	SERVERBKP:      Remote Server to send the backup file

	SERVERBKPUSER:  Remote Server user access

	SERVERBKPPATH:  Remote Server destination path, must be the same in "/etc/rsyncd.conf"
                        Read Examples in https://download.samba.org/pub/rsync/rsyncd.conf.html

Example:

	DBUSER="root"
	DBPASSWORD="pass1234"
	DBARRAY="zabbix nagios cacti"
	DUMPFILENAME="mysqldatabase"
	DUMPPATH="/var/mydumps"
	DUMPRETENTION="5"
	DBDUMPLOG="dbdump.log"
	SERVERBKP="faraway.com"
	SERVERBKPUSER="rsync"
	SERVERBKPPATH="backupdir"

Is possible to create dynamic configurations with subshell, for example:

	Files wich was rotated with the date from one day ago.
	BKPDIRNFILES="etc usr/local/bin var/log/nginx/*$(date +%Y%m%d -d "yesterday")*"

	Daily 'backup directories' in the destination server that will be created automatically.
	SERVERBKPPATH="backupdir/$hostname/$(date +%Y-%m-%d-%H)"
