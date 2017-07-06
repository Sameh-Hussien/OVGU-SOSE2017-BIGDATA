* The full teragen command and job output


```
$ { time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen -Ddfs.blocksize=16777216 -Dmapreduce.job.maps=6 65536000 /user/neymar/tgen640/teragen.data 2> mapred-job.txt ; } 2> time.txt

	17/07/06 13:18:46 INFO client.RMProxy: Connecting to ResourceManager at ip-172-3
	1-12-245.eu-central-1.compute.internal/172.31.12.245:8032
	17/07/06 13:18:47 INFO terasort.TeraGen: Generating 65536000 using 6
	17/07/06 13:18:47 INFO mapreduce.JobSubmitter: number of splits:6
	17/07/06 13:18:47 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_14
	99357693834_0002
	17/07/06 13:18:47 INFO impl.YarnClientImpl: Submitted application application_14
	99357693834_0002
	17/07/06 13:18:47 INFO mapreduce.Job: The url to track the job: http://ip-172-31
	-12-245.eu-central-1.compute.internal:8088/proxy/application_1499357693834_0002/
	
	17/07/06 13:18:47 INFO mapreduce.Job: Running job: job_1499357693834_0002
	17/07/06 13:18:54 INFO mapreduce.Job: Job job_1499357693834_0002 running in uber
	mode : false
	17/07/06 13:18:54 INFO mapreduce.Job:  map 0% reduce 0%
	17/07/06 13:19:13 INFO mapreduce.Job:  map 21% reduce 0%
	17/07/06 13:19:15 INFO mapreduce.Job:  map 29% reduce 0%
	17/07/06 13:19:19 INFO mapreduce.Job:  map 34% reduce 0%
	17/07/06 13:19:20 INFO mapreduce.Job:  map 36% reduce 0%
	17/07/06 13:19:21 INFO mapreduce.Job:  map 37% reduce 0%
	17/07/06 13:19:25 INFO mapreduce.Job:  map 42% reduce 0%
	17/07/06 13:19:26 INFO mapreduce.Job:  map 45% reduce 0%
	17/07/06 13:19:31 INFO mapreduce.Job:  map 51% reduce 0%
	17/07/06 13:19:32 INFO mapreduce.Job:  map 53% reduce 0%
	17/07/06 13:19:37 INFO mapreduce.Job:  map 59% reduce 0%
	17/07/06 13:19:39 INFO mapreduce.Job:  map 62% reduce 0%
	17/07/06 13:19:44 INFO mapreduce.Job:  map 68% reduce 0%
	17/07/06 13:19:45 INFO mapreduce.Job:  map 71% reduce 0%
	17/07/06 13:19:50 INFO mapreduce.Job:  map 76% reduce 0%
	17/07/06 13:19:51 INFO mapreduce.Job:  map 80% reduce 0%
	17/07/06 13:19:55 INFO mapreduce.Job:  map 82% reduce 0%
	17/07/06 13:19:56 INFO mapreduce.Job:  map 84% reduce 0%
	17/07/06 13:19:57 INFO mapreduce.Job:  map 87% reduce 0%
	17/07/06 13:20:02 INFO mapreduce.Job:  map 92% reduce 0%
	17/07/06 13:20:03 INFO mapreduce.Job:  map 94% reduce 0%
	17/07/06 13:20:05 INFO mapreduce.Job:  map 95% reduce 0%
	17/07/06 13:20:06 INFO mapreduce.Job:  map 96% reduce 0%
	17/07/06 13:20:08 INFO mapreduce.Job:  map 98% reduce 0%
	17/07/06 13:20:09 INFO mapreduce.Job:  map 100% reduce 0%
	17/07/06 13:20:09 INFO mapreduce.Job: Job job_1499357693834_0002 completed succe
	ssfully
	17/07/06 13:20:09 INFO mapreduce.Job: Counters: 33
			File System Counters
					FILE: Number of bytes read=0
					FILE: Number of bytes written=766230
					FILE: Number of read operations=0
					FILE: Number of large read operations=0
					FILE: Number of write operations=0
					HDFS: Number of bytes read=511
					HDFS: Number of bytes written=6553600000
					HDFS: Number of read operations=24
					HDFS: Number of large read operations=0
					HDFS: Number of write operations=12
			Job Counters
					Launched map tasks=6
					Other local map tasks=6
					Total time spent by all maps in occupied slots (ms)=410272
					Total time spent by all reduces in occupied slots (ms)=0
					Total time spent by all map tasks (ms)=410272
					Total vcore-milliseconds taken by all map tasks=410272
					Total megabyte-milliseconds taken by all map tasks=420118528
			Map-Reduce Framework
					Map input records=65536000
					Map output records=65536000
					Input split bytes=511
					Spilled Records=0
					Failed Shuffles=0
					Merged Map outputs=0
					GC time elapsed (ms)=1045
					CPU time spent (ms)=118330
					Physical memory (bytes) snapshot=2006614016
					Virtual memory (bytes) snapshot=9402339328
					Total committed heap usage (bytes)=2003304448
					Peak Map Physical memory (bytes)=390213632
					Peak Map Virtual memory (bytes)=1573806080
			org.apache.hadoop.examples.terasort.TeraGen$Counters
					CHECKSUM=140750829423462787
			File Input Format Counters
					Bytes Read=0
			File Output Format Counters
					Bytes Written=6553600000
```

* The result of the time command

```
	real    1m25.401s
	user    0m6.575s
	sys     0m0.383s
```

* The command and output of hdfs dfs -ls /user/neymar/tgen640

```
$ hdfs dfs -ls /user/neymar/tgen640

	Found 1 items
	drwxr-xr-x   - neymar merengues          0 2017-07-06 13:20 /user/neymar/tgen640/teragen.data
```

* The command and output to show how many blocks are stored under this directory

```
$ hdfs fsck /user/neymar/tgen640 -blocks

	Connecting to namenode via http://ip-172-31-12-245.eu-central-1.compute.internal
	:50070
	FSCK started by neymar (auth:SIMPLE) from /172.31.6.98 for path /user/neymar/tge
	n640 at Thu Jul 06 13:27:53 EDT 2017
	.......Status: HEALTHY
	Total size:    6553600000 B
	Total dirs:    2
	Total files:   7
	Total symlinks:                0
	Total blocks (validated):      396 (avg. block size 16549494 B)
	Minimally replicated blocks:   396 (100.0 %)
	Over-replicated blocks:        0 (0.0 %)
	Under-replicated blocks:       0 (0.0 %)
	Mis-replicated blocks:         0 (0.0 %)
	Default replication factor:    3
	Average block replication:     3.0
	Corrupt blocks:                0
	Missing replicas:              0 (0.0 %)
	Number of data-nodes:          4
	Number of racks:               1
	FSCK ended at Thu Jul 06 13:27:53 EDT 2017 in 13 milliseconds
	
	
	The filesystem under path '/user/neymar/tgen640' is HEALTHY
```