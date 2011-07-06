Pig & Cassandra
---------------

*Outline for CassandraDC Meetup Talk, 07/06/2011*

* What's Pig?
    * [Apache Pig](http://pig.apache.org/ "Pig")
    
		```
		-- Counts all the rows in a column family  
		rows = LOAD 'cassandra://ks/cf' USING CassandraStorage();  
		countthis = GROUP rows ALL;  
		countedrows = FOREACH countthis GENERATE COUNT(rows.$0);  
		dump countedrows;  
		```

	* Hive:SQL :: Pig:SQL execution plan

* How does it work with Cassandra?

	* Leverages Cassandra/Hadoop MapRed classes (obviously)
		* ColumnFamilyInputFormat
		* ColumnfamilyOutputFormat
		* CassandraStorage Load/Store Func.  
			`STORE stuff INTO 'cassandra://ks/cf' using CassandraStorage();`
		
	* Configuration can be tricky
		* In mapred-site.xml:
		
		```
		<property>  
			<name>cassandra.thrift.port</name>  
			<value>9160</value>  
		</property>  
		<property>  
			<name>cassandra.thrift.address</name>  
			<value>hostname</value>  
		</property>  
		<property>  
			<name>cassandra.partitioner.class</name>  
			<value>org.apache.cassandra.dht.RandomPartitioner</value>  
		</property>  
		```
		
		* Suggest giving [Brisk](http://www.datastax.com/products/brisk) a spin.

* Real-World use
	* Only useful if you have to iterate over ALL your cassandra data AND
	* You don't have a copy of the data in Hadoop
	* Why?
		* If data is also in Hadoop, HDFS offers much faster reads due to much larger sequential blocks.
		* Right now, you can't narrow your pig job with an indexed search
			* [CASSANDRA-1600](https://issues.apache.org/jira/browse/CASSANDRA-1600)
			* [CASSANDRA-1125](https://issues.apache.org/jira/browse/CASSANDRA-1125)
			* [CASSANDRA-2246](https://issues.apache.org/jira/browse/CASSANDRA-2246)
		* When that's fixed, pig will really be useful. (Hive too)

* Resources
	* [SVN](https://svn.apache.org/repos/asf/cassandra/trunk/contrib/pig/)
	* $BRISK_HOME/resources/pig/examples


&copy; 2011 Matt Kennedy, All Rights Reserved.