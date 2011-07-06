Brisk
-----
*Outline for CassandraDC Meetup Talk, 07/06/2011*


* Brisk is a Hadoop Distro from DataStax
* I don't work for DataStax, I just think this is a good idea.
* Brisk == (Cassandra 0.8+) + (Hadoop 0.20.203+)
* Replaces HDFS
	* No NameNode
	* No Heap limits
	* CassandraFS (CFS) - can be used as a general purpose CFS, ala S3.
* JobTracker auto-nominated
* Includes a Hive metastore, no separate database required.


[Brisk@GitHub](https://github.com/riptano/brisk)

&copy; 2011 Matt Kennedy, All Rights Reserved.