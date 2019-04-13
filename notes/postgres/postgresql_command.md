# Postgresql 9.4


### psql Commands
```
[root@c20 15:47:43 /var/lib/pgsql]# su - postgres
[postgres@c20 15:47:50 ~]$
[postgres@c20 15:48:38 ~]$ psql
psql (9.4.21)
Type "help" for help.

postgres=# help
You are using psql, the command-line interface to PostgreSQL.
Type:  \copyright for distribution terms
       \h for help with SQL commands
       \? for help with psql commands
       \g or terminate with semicolon to execute query
       \q to quit
postgres=# select version();
                                                    version                                                     
----------------------------------------------------------------------------------------------------------------
 PostgreSQL 9.4.21 on x86_64-unknown-linux-gnu, compiled by gcc (GCC) 4.8.5 20150623 (Red Hat 4.8.5-36), 64-bit
(1 row)

postgres=# SELECT current_date;
    date    
------------
 2019-03-22
(1 row)

postgres=# SELECT current_time;
       timetz       
--------------------
 16:22:50.334087+08
(1 row)

postgres=#



postgres=#  \q

[postgres@c20 16:19:32 ~]$ psql mydb
psql (9.4.21)
Type "help" for help.

mydb=#
```
