#teragen
#Command
{ time hadoop jar /usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen -Ddfs.blocksize=16777216 -Dmapreduce.job.maps=6 50000000 /user/Sameh-Manaa/teragen-5GB.data 2> mapred-job.txt ; } 2> time.txt
#Result
real	7m42.702s
user	0m10.183s
sys	0m1.683s


#terasort
#Command
{ time hadoop jar /usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar terasort /user/Sameh-Manaa/teragen-5GB /user/Sameh-Manaa/terasort-5GB 2> mapred-job.txt ; } 2>> time.txt
#Result
real	67m40.446s
user	0m18.108s
sys	0m4.398s
