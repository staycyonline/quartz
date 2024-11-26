Tags: #SQL
Related to: #hacking , #ejpt
See also: 
Index: [[📁EJPTv2 - INDEX]] - index location 

#### Summary
Intro to SQL hacking

#### Intro

#### MySQL

MySQL Resides usually on port 3306

Issues - Null password
`mysql -h <ip> -u root` 

#### SQL cmds
`show databases;`
`use <db_name>;`
`select load_file("path/to/file")`


#### msfconsole scanners
`auxilliary/scanner/mysql/mysql_writable_dirs` - writable directories using sql

`auxilliary/scanner/mysql/mysql_hashdump` - gets a lot of hashes

## nmap script

`mysql-empty-password`

`mysql-info

INTERACTIVE CLIENT IS NOT GOOD CAPABILITY

`mysql-users`
`mysql-databases`
`mysql-variables`
`mysql-audit`
`mysql-dump-hashes`
`mysql-query`


#### Dictionary attack

msfconsole
	`auxiliary/scanner/mysql/mysql_login`

hydra
`hydra -l username -P /path/to/wordlist ip port`

There are ither ways 

#### MSSQL

Gnerally resides on 1433

nmap scripts
	`ms-sql-info`
	`ms-sql-ntlm-info`
	`ms-sql-brute`
	`ms-sql-empty-password`
	`ms-sql-query`
	`ms-sql-dumphashes`
	`ms-sql-xp-cmdshell`	

metasploit
	`/auxiliary/scanner/mssql/mssql_login`
	`/auxiliary/admin/mssql/mssql_enum`
	`/auxiliary/admin/mssql/mssql_enum_sql_logins`

	/auxiliary/admin/mssql/mssql_exec`

	`/auxiliary/admin/mssql/mssql_enum_domain_accounts`