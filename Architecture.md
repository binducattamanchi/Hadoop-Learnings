# Architecture


The Hadoop architecture is a package of the file system, MapReduce engine and the HDFS (Hadoop Distributed File System). The MapReduce engine can be MapReduce/MR1 or YARN/MR2.
A Hadoop cluster consists of a single master and multiple slave nodes. 
The master node includes Job Tracker, Task Tracker, NameNode, and DataNode whereas the slave node includes DataNode and TaskTracker.

![image](https://user-images.githubusercontent.com/32897934/124355150-602af880-dc2d-11eb-9e8b-fa23f35621fe.png)


* HDFS architecture

 ![image](https://user-images.githubusercontent.com/32897934/124354975-7a180b80-dc2c-11eb-9d88-1e7d7dda9a74.png)

**NameNode**

1. Stores metadata for the files, like the directory structure of a typical FS.
2. The server holding the NameNode instance is quite crucial, as there is only one.
3. Transaction log for file deletes/adds,etc.Does not use transaction for whole blocks or file-streams, only metadata.
4. Handles creation of more replica blocks when necessary after a DataNode failure.
DataNode

**Stores the actual data in HDFS**

1. Can run on any underlying filesystem (ext3/4, NTFS, etc)
2. Notifies NameNode of what blocks it has
3. NameNode replicates blocks 2x in local rack, 1x elsewhere

* MapReduce architecture

 ![image](https://user-images.githubusercontent.com/32897934/124354992-8a2feb00-dc2c-11eb-84e5-485c79014d41.png)

**MapReduce Engine**

1. JobTracker & TaskTracker
2. JobTracker splits up data into smaller tasks(“Map”) and sends it to the TaskTracker process in each node
3. TaskTracker reports back to the JobTracker node and reports on job progress, sends data (“Reduce”) or requests new jobs
4. None of these components are necessarily limited to using HDFS.
5. Many other distributed file-systems with quite different architecture work
6. Many other software packages besides Hadoop’s MapReduce platform make use of HDFS

* Secondary Namenode

![image](https://user-images.githubusercontent.com/32897934/124355707-3fb06d80-dc30-11eb-9b59-983d3bec1d5a.png)

Secondary NameNode downloads the Fsimage file and edit logs file from NameNode.
It periodically applies edit logs to Fsimage and refreshes the edit logs. 
The updated Fsimage is then sent to the NameNode so that NameNode doesn’t have to re-apply the edit log records during its restart. 
This keeps the edit log size small and reduces the NameNode restart time.
If the NameNode fails, the last save Fsimage on the secondary NameNode can be used to recover file system metadata. 
The secondary NameNode performs regular checkpoints in HDFS.
