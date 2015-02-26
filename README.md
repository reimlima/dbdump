dbdump
--------------------------------------------------------------------------------

Backup and purge script for MySQL.


Notice
--------------------------------------------------------------------------------

This script was tested and work well in:

* Linux
	GNU bash, version 4.1.2(1)-release (x86_64-redhat-linux-gnu)

Changelog
--------------------------------------------------------------------------------

2015-02-21	- v2	- First Stable Release

2015-02-24	- v2.1	- Added "--single-transaction" parameter for "non lock" entire database

2015-02-26	- v2.2	- Removed unnecessary lock file
			- Better comment about conf file

How to use it
--------------------------------------------------------------------------------

CONF FILE:

Just  fill  the  configuration  file  with  the  values  for DBUSER, DBPASSWORD,
DBARRAY, DUMPFILENAME, DUMPPATH, DUMPRETENTION, DBDUMPLOG, then run the script.

Legend:

	DBUSER:			MySQL Access Login
	
	DBPASSWORD: 	MySQL Access Password
	
	DBARRAY:		Databases to Backup
					fill it in format like => "db1 db2 dbN"
					Empty = "All Databases"
					
	DUMPFILENAME:	Name of Dump File
	
	DUMPPATH:		Path to dumpfile, no slash in the end
	
	DUMPRETENTION:	Time to retention in days,
					older files than "DUMPRETENTION" will be removed
					
	DBDUMPLOG:		Log File

Example:

	DBUSER="root"
	DBPASSWORD="pass1234"
	DBARRAY="zabbix nagios cacti"
	DUMPFILENAME="mysqldatabase"
	DUMPPATH="/var/mydumps"
	DUMPRETENTION="5"
	DBDUMPLOG="dbdump.log"
