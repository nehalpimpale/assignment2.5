# assignment2.5

1.Explain what is a cluster and what is a hadoop cluster

Cluster: Normally any set of loosely connected or tightly connected computers that work together as a single system is called Cluster. In simple words, a computer cluster used for Hadoop is called Hadoop Cluster.

Hadoop cluster is a special type of computational cluster designed for storing and analyzing vast amount of unstructured data in a distributed computing environment. These clusters run on low cost commodity computers.

Hadoop Cluster - Architecture and Components

In this case Hadoop Cluster would consists of 110 different racks Each rack would have around 40 slave machine At the top of each rack there is a rack switch Each slave machine(rack server in a rack) has cables coming out it from both the ends Cables are connected to rack switch at the top which means that top rack switch will have around 80 ports There are global 8 core switches The rack switch has uplinks connected to core switches and hence connecting all other racks with uniform bandwidth, forming the Cluster In the cluster, you have few machines to act as Name node and as JobTracker. They are referred as Masters. These masters have different configuration favoring more DRAM and CPU and less local storage. The majority of the machines acts as DataNode and Task Trackers and are referred as Slaves. These slave nodes have lots of local disk storage and moderate amounts of CPU and DRAM

Core Components of Hadoop Cluster:

Hadoop cluster has 3 components: Client Master Slave The role of each components are shown in the below image.

Masters:

The Masters consists of 3 components NameNode, Secondary Node name and JobTracker.

NameNode: NameNode does NOT store the files but only the file's metadata. In later section we will see it is actually the DataNode which stores the files.

NameNode oversees the health of DataNode and coordinates access to the data stored in DataNode. Name node keeps track of all the file system related information such as to Which section of file is saved in which part of the cluster Last access time for the files User permissions like which user have access to the file JobTracker: JobTracker coordinates the parallel processing of data using MapReduce.

Secondary Name Node: Don't get confused with the name "Secondary". Secondary Node is NOT the backup or high availability node for Name node.

The job of Secondary Node is to contact NameNode in a periodic manner after certain time interval(by default 1 hour). NameNode which keeps all filesystem metadata in RAM has no capability to process that metadata on to disk. So if NameNode crashes, you lose everything in RAM itself and you don't have any backup of filesystem. What secondary node does is it contacts NameNode in an hour and pulls copy of metadata information out of NameNode. It shuffle and merge this information into clean file folder and sent to back again to NameNode, while keeping a copy for itself. Hence Secondary Node is not the backup rather it does job of housekeeping. In case of NameNode failure, saved metadata can rebuild it easily.

Slaves:

Slave nodes are the majority of machines in Hadoop Cluster and are responsible to Store the data Process the computation


2.What is meant by a Rack and explain the rack arrangement in a hadoop cluster

 Hadoop has two major components build with. They are namely

The Hadoop distributed file system (HDFS) – A distributed file system for Hadoop also support IBM GPFS-FPO.
The MapReduce component – A popular framework used for performing calculations on the data inside distributed file system.
Here the Hadoop Rack is a set of 30 or 40 nodes physically stored close together. These nodes are connected to the same network using a switch. Similarly Hadoop cluster is a collection of racks. I refer this blog post for detailed information about Hadoop racks.

What is rack awareness in Hadoop?

Hadoop Rack awareness is a setup to improve network traffic in the time of reading or writing HDFS files. If you have Hadoop clusters more than 30 to 40 nodes Hadoop rack aware configuration helpful to you. Because data transmitting between two nodes on the same rack is more efficient than data transfer between different racks. 

Hadoop rack awareness helps you to define manually the rack number of each slave datanode in the cluster. So far Hadoop has the concept functioning behind Rack Awareness. We are manually defined the rack numbers because we can prevent the data loss and enhance the network performance.
Hadoop Rack AwarenessTherefore the each block of data will transmitted to multiple machines. It prevent if some machine failure, we not losing all copies of data.
Never lose of data if entire rack fails.
If possible the system can keep bulky flows in rack.
Mostly the rack is higher bandwidth and lower latency.
