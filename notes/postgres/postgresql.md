# PostgreSQL

https://www.postgresql.org/docs/9.4/index.html

## Install
```
https://www.postgresql.org/download/linux/redhat/
https://www.postgresql.org/download/linux/ubuntu/

yum install https://download.postgresql.org/pub/repos/yum/9.4/redhat/rhel-7-x86_64/pgdg-centos94-9.4-3.noarch.rpm
yum install postgresql94 postgresql94-server
systemctl enable postgresql-9.4
systemctl start postgresql-9.4

#RHEL/CentOS/SL/OL 7	9.2 (also supplies package rh-postgresql95 and rh-postgresql94 via SCL)
#/usr/lib/tmpfiles.d/postgresql-9.4.conf
#/usr/lib/systemd/system/postgresql-9.4.service
#/etc/sysconfig/pgsql
#/etc/pam.d/postgresql
```


## Install on ubuntu
```
18.04
deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main

16.04
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main

14.04
deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main


wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-10

```



## Concepts
```
Server forks a new process for each client connection.
Database cluster: database storage area on disk. (The SQL standard uses the term catalog cluster.)
Some PostgreSQL language features are extensions to the standard.
If possible, mount the NFS file system synchronously (without caching) to avoid this hazard.
  Also, soft-mounting the NFS file system is not recommended.
```


## Admin commands
```
#init db
/usr/pgsql-9.4/bin/postgresql94-setup initdb [ /var/lib/pgsql/9.4/data/ ]
/usr/pgsql-9.4/bin/pg_ctl -D /var/lib/pgsql/9.4/data/ initdb

#start service
postgres -D /usr/local/pgsql/data
postgres -D /usr/local/pgsql/data > logfile 2>&1 &
pg_ctl start -l logfile
su postgres -c 'pg_ctl start -D /usr/local/pgsql/data -l serverlog'

#shutdown
systemctl stop postgresql-9.4.service
pg_ctl stop
pg_ctl reload

##kill sigs:
##SIGTERM
##Smart Shutdown mode: disallows new connections, but lets existing sessions end their work normally.
##
##SIGINT
##Fast Shutdown mode:  disallows new connections and all server process abort their current transactions and exit promptly.
##
##SIGQUIT
##Immediate Shutdown mode: terminates and kill all child processes and wait for them to terminate. This will lead to recovery (by replaying the WAL log) upon next start-up.
##
##Use pg_terminate_backend(pid int) 	to terminate a child process
##SIGHUP
##The configuration file is reread whenever the main server process receives a SIGHUP signal. pg_reload_conf()


#upgrade
##minor upgrades, like 8.4.2 -> 8.4.6 , just upgrade it.
##major upgrades, like 8.4.6 -> 9.4.2 , pg_upgrade and read 'Release Notes.Migration'
##logical backup tool like pg_dumpall is a better choice.

#backup & restore all
pg_dumpall > outputfile
/usr/local/pgsql/bin/psql -d postgres -f outputfile

#backup to another instance
pg_dumpall -p 5432 | psql -d postgres -p 5433



#creates db
createdb mydb
```

## Managing Kernel Resources
https://www.postgresql.org/docs/9.4/kernel-resources.html

## Secure TCP/IP Connections with SSL
https://www.postgresql.org/docs/9.4/ssl-tcp.html


## Ports and files
```
[root@c20 15:41:18 ~]# nst l |grep postgres
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      24399/postgres      
tcp6       0      0 ::1:5432                :::*                    LISTEN      24399/postgres

[root@c20 15:40:25 ~]# ll -a /var/run/postgresql/
total 4.0K
srwxrwxrwx  1 postgres postgres   0 2019-03-22 14:57 .s.PGSQL.5432
-rw-------  1 postgres postgres  66 2019-03-22 14:57 .s.PGSQL.5432.lock

[root@c20 15:38:44 ~]# ll /var/lib/pgsql/9.4/data/
total 56K
drwx------ 5 postgres postgres   41 2019-03-22 13:58 base
drwx------ 2 postgres postgres 4.0K 2019-03-22 13:59 global
drwx------ 2 postgres postgres    6 2019-03-22 13:58 log
drwx------ 2 postgres postgres   18 2019-03-22 13:58 pg_clog
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_dynshmem
-rw------- 1 postgres postgres 4.2K 2019-03-22 13:58 pg_hba.conf	#Client Authentication Configuration File
-rw------- 1 postgres postgres 1.6K 2019-03-22 13:58 pg_ident.conf
drwx------ 2 postgres postgres   32 2019-03-22 13:59 pg_log
drwx------ 4 postgres postgres   39 2019-03-22 13:58 pg_logical
drwx------ 4 postgres postgres   36 2019-03-22 13:58 pg_multixact
drwx------ 2 postgres postgres   18 2019-03-22 13:59 pg_notify
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_replslot
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_serial
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_snapshots
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_stat
drwx------ 2 postgres postgres   63 2019-03-22 15:38 pg_stat_tmp
drwx------ 2 postgres postgres   18 2019-03-22 13:58 pg_subtrans
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_tblspc
drwx------ 2 postgres postgres    6 2019-03-22 13:58 pg_twophase
-rw------- 1 postgres postgres    4 2019-03-22 13:58 PG_VERSION
drwx------ 3 postgres postgres   60 2019-03-22 13:58 pg_xlog
-rw------- 1 postgres postgres   88 2019-03-22 13:58 postgresql.auto.conf
-rw------- 1 postgres postgres  21K 2019-03-22 13:58 postgresql.conf
-rw------- 1 postgres postgres   59 2019-03-22 13:59 postmaster.opts
-rw------- 1 postgres postgres   96 2019-03-22 13:59 postmaster.pid

[postgres@c20 15:57:35 ~]$ ll /usr/pgsql-9.4/bin/
total 7.9M
-rwxr-xr-x 1 root root  62K 2019-02-13 13:24 clusterdb
-rwxr-xr-x 1 root root  62K 2019-02-13 13:24 createdb
-rwxr-xr-x 1 root root  86K 2019-02-13 13:24 createlang
-rwxr-xr-x 1 root root  62K 2019-02-13 13:24 createuser
-rwxr-xr-x 1 root root  58K 2019-02-13 13:24 dropdb
-rwxr-xr-x 1 root root  86K 2019-02-13 13:24 droplang
-rwxr-xr-x 1 root root  58K 2019-02-13 13:24 dropuser
-rwxr-xr-x 1 root root 100K 2019-02-13 13:24 initdb
-rwxr-xr-x 1 root root  20K 2019-02-13 13:24 pg_archivecleanup
-rwxr-xr-x 1 root root  71K 2019-02-13 13:24 pg_basebackup
-rwxr-xr-x 1 root root  58K 2019-02-13 13:24 pgbench
-rwxr-xr-x 1 root root  29K 2019-02-13 13:24 pg_config
-rwxr-xr-x 1 root root  29K 2019-02-13 13:24 pg_controldata
-rwxr-xr-x 1 root root  41K 2019-02-13 13:24 pg_ctl
-rwxr-xr-x 1 root root 339K 2019-02-13 13:24 pg_dump
-rwxr-xr-x 1 root root  79K 2019-02-13 13:24 pg_dumpall
-rwxr-xr-x 1 root root  58K 2019-02-13 13:24 pg_isready
-rwxr-xr-x 1 root root  46K 2019-02-13 13:24 pg_receivexlog
-rwxr-xr-x 1 root root  37K 2019-02-13 13:24 pg_resetxlog
-rwxr-xr-x 1 root root 144K 2019-02-13 13:24 pg_restore
-rwxr-xr-x 1 root root  21K 2019-02-13 13:24 pg_test_fsync
-rwxr-xr-x 1 root root  16K 2019-02-13 13:24 pg_test_timing
-rwxr-xr-x 1 root root 111K 2019-02-13 13:24 pg_upgrade
-rwxr-xr-x 1 root root  50K 2019-02-13 13:24 pg_xlogdump
-rwxr-xr-x 1 root root 5.6M 2019-02-13 13:24 postgres
-rwxr-xr-x 1 root root 2.2K 2019-02-13 13:24 postgresql94-check-db-dir
-rwxr-xr-x 1 root root 9.3K 2019-02-13 13:24 postgresql94-setup
lrwxrwxrwx 1 root root    8 2019-03-22 13:53 postmaster -> postgres
-rwxr-xr-x 1 root root 464K 2019-02-13 13:24 psql
-rwxr-xr-x 1 root root  62K 2019-02-13 13:24 reindexdb
-rwxr-xr-x 1 root root  62K 2019-02-13 13:24 vacuumdb
[postgres@c20 15:57:55 ~]$

```

## Setting Parameters
- postgresql.conf
- One parameter is specified per line. The equal sign between name and value is optional. Whitespace is insignificant (except within a quoted parameter value) and blank lines are ignored. Hash marks (#) designate the remainder of the line as a comment.
- All parameter names are **case-insensitive** .
- The latest parameters override previous ones.
- Boolean: Values can be written as on, off, true, false, yes, no, 1, 0 (all **case-insensitive**) or any unambiguous prefix of one of these.
- String: In general, enclose the value in single quotes, doubling any single quotes within the value.
- Numeric (integer and floating point): A decimal point is permitted only for floating-point parameters.
- Numeric with Unit:The unit name is **case-sensitive**, and there can be whitespace between the numeric value and the unit.
  - Valid memory units are kB (kilobytes), MB (megabytes), GB (gigabytes), and TB (terabytes). The multiplier for memory units is 1024, not 1000.
  - Valid time units are ms (milliseconds), s (seconds), min (minutes), h (hours), and d (days).
- Enumerated: Enum parameter values are **case-insensitive** .
- ALTER SYSTEM command is equivalent to editing postgresql.conf

- interact with session-local configuration settings:
```
SELECT * FROM pg_settings;
SHOW ALL;
SHOW WORK_MEM;
SET WORK_MEM TO 8MB;
```

- postgres starts with parameters, overrides but does not change postgresql.conf
`postgres -c log_connections=yes -c log_destination='syslog'`

- client session with env
`env PGOPTIONS="-c geqo=off -c statement_timeout=5min" psql`

- include conf files
```
include_dir = 'conf.d'                 # include files ending in '.conf' from directory 'conf.d' in alphabetic order.
include_if_exists = 'exists.conf'      # include file only if it exists
include = 'special.conf'               # include file
```
- accessible to network users
`listen_addresses = 'localhost,192.168.1.20'`


Others:
https://www.postgresql.org/docs/9.4/runtime-config.html


## Client Access
```
Env:
PGHOST=
PGPORT=
PGUSER=
PGDATA=

psql prompt =#	Super user
psql prompt =>	Normal user
```

### pg_hba.conf
`host    all             all             192.168.1.0/24          md5`

Bash:
`psql -h 192.168.1.20 -p 5432 -U nrole`

 TYPE 				| DATABASE    |    USER      |      ADDRESS        |  METHOD  
 ---  				|  ---        |   ---        |        ---          |   ---    
**local** :	unix sockets<br>if no local, sockets disallowed<br>**host** : TCP/IP with/without SSL<br>**hostssl** : TCP/IP SSL only<br>**hostnossl** : TCP/IP no SSL only | all<br>sameuser<br>samerole<br>replication<br>db1,db2,db3<br>@dbs.file | all<br>(+)user1,role1,user2<br>@users.file | IP/CIDR_MASK<br>IP MASK | **trust**<br>**reject**<br>**md5** : double-MD5-hashed<br>**password** : unencrypted<br>**peer** : only local<br>**cert , gss , sspi , ident , ldap , radius , pam**



## pgAdmin
#sudo apt-get install curl ca-certificates
curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo echo 'deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg 9.4' > /etc/apt/sources.list.d/pgdg.list
sudo apt update; sudo apt install pgadmin3
sudo apt install pgadmin3
  Suggested packages:
    postgresql-contrib postgresql-10 postgresql-doc-10
  The following NEW packages will be installed:
    libjs-underscore pgadmin3 pgadmin3-data pgagent postgresql-client postgresql-client-10 postgresql-client-common

