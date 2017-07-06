* Hostname

```
	ip-172-31-6-98.eu-central-1.compute.internal
```

* The command and output for display your database server's version

```
	MariaDB [(none)]> SHOW VARIABLES like 'VERSION';
	+---------------+----------------+
	| Variable_name | Value          |
	+---------------+----------------+
	| version       | 5.5.55-MariaDB |
	+---------------+----------------+
	1 row in set (0.00 sec)
```

* The command and output for listing your created databases

```
	MariaDB [(none)]> show databases;
	+--------------------+
	| Database           |
	+--------------------+
	| information_schema |
	| hive               |
	| hue                |
	| mysql              |
	| oozie              |
	| performance_schema |
	| rman               |
	| scm                |
	| sentry             |
	+--------------------+
	9 rows in set (0.00 sec)
```