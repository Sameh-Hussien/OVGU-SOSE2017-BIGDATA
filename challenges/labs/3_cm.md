* The command and output for `hdfs dfs -ls /user`

```
$ hdfs dfs -ls /user

	Found 6 items
	drwxrwxrwx   - mapred hadoop              0 2017-07-06 12:14 /user/history
	drwxrwxr-t   - hive   hive                0 2017-07-06 12:15 /user/hive
	drwxrwxr-x   - hue    hue                 0 2017-07-06 12:16 /user/hue
	drwxr-xr-x   - hdfs   supergroup          0 2017-07-06 12:25 /user/neymar
	drwxrwxr-x   - oozie  oozie               0 2017-07-06 12:16 /user/oozie
	drwxr-xr-x   - hdfs   supergroup          0 2017-07-06 12:25 /user/ronaldo
```


* The output from the CM API call ../api/v14/hosts

```
{
  "items" : [ {
    "hostId" : "f481b378-40af-4419-9bd2-3d43ef0c3435",
    "ipAddress" : "172.31.12.245",
    "hostname" : "ip-172-31-12-245.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-6-98.eu-central-1.compute.internal:7180/cmf/hostRedirect/f481b378-40af-4419-9bd2-3d43ef0c3435",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15664758784
  }, {
    "hostId" : "a32d24dc-9101-478b-babb-1d9487928d7f",
    "ipAddress" : "172.31.15.205",
    "hostname" : "ip-172-31-15-205.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-6-98.eu-central-1.compute.internal:7180/cmf/hostRedirect/a32d24dc-9101-478b-babb-1d9487928d7f",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15664758784
  }, {
    "hostId" : "4a0b60a8-7b89-4c52-b677-30a040a29807",
    "ipAddress" : "172.31.4.25",
    "hostname" : "ip-172-31-4-25.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-6-98.eu-central-1.compute.internal:7180/cmf/hostRedirect/4a0b60a8-7b89-4c52-b677-30a040a29807",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15664758784
  }, {
    "hostId" : "b8c337a0-fc77-4a0c-bbd9-b88bb77c69c1",
    "ipAddress" : "172.31.6.98",
    "hostname" : "ip-172-31-6-98.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-6-98.eu-central-1.compute.internal:7180/cmf/hostRedirect/b8c337a0-fc77-4a0c-bbd9-b88bb77c69c1",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15664758784
  }, {
    "hostId" : "6571c40d-0b07-4521-ac35-2d802f315b69",
    "ipAddress" : "172.31.7.19",
    "hostname" : "ip-172-31-7-19.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-6-98.eu-central-1.compute.internal:7180/cmf/hostRedirect/6571c40d-0b07-4521-ac35-2d802f315b69",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15664758784
  } ]
}
```