# Hadoop-installation 
Hadoop installation steps in mac 



## 1. Install Hadoop 3.0.0 and set passwordless ssh key. (for more details, check reference link at end of file)
  - Hadoop nodes communicate between each other frequently. Allow remote access to the user where this hadoop is installed. 

## 2. Cd to Hadoop Folder to configure hadoop environment. 
  - Configuration files locations In linux: /usr/local/Cellar/hadoop/3.0.0/libexec/etc/hadoop

### 1. Open hadoop-env.sh and export your system java path, Hadoop installation path 
```xml
  export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-9.0.1.jdk/Contents/Home
  export HADOOP_PREFIX=/usr/local/Cellar/hadoop/3.0.0
```
### 2. Open core-site.xml and add below data:

```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
</configuration>
```
### 3. Open hdfs-site.xml and add below data:
```xml
<configuration>

  <property>
   <name>dfs.replication</name>
   <value>1</value>
   <description> How many copies of data our hadoop will have. Value defines how many copies </description>
  </property>
</configuration>
```
### 4. Open mapred-site.xml and add below data:
```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
    <description> Mapreduce - maps the data and reduces that data to give it to you. This is done by deamon. This tracks all jobs running in hadoop cluster. </description>
  </property>
</configuration>
```
### 5. Open yarn-site.xml and add below data: 
```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>

</configuration>
```

### 6. Move to /usr/local/Cellar/hadoop/3.0.0 and start name node as 
- bin/hadoop namenode -format 

### 7. start or stop the hadoop. 

- Start - '/usr/local/Cellar/hadoop/3.0.0/sbin/start-dfs.sh'  or   '/usr/local/Cellar/hadoop/3.0.0/sbin/start-all.sh'
- Stop - '/usr/local/Cellar/hadoop/3.0.0/sbin/stop-dfs.sh'   or    '/usr/local/Cellar/hadoop/3.0.0/sbin/stop-all.sh'


### Output after succesful hadoop installation looks like below:
```xml
krishnas-mbp:sbin krishna.damarla$ ./start-dfs.sh 
Starting namenodes on [localhost]
Starting datanodes
Starting secondary namenodes [krishnas-mbp.widas.de]
2018-04-10 14:14:40,129 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
```
(Last message is just a warning. Can be neglected) 

### jps in terminal shows all the processes running as below:
```xml
898 
9493 DataNode
10553 Jps
9630 SecondaryNameNode
9391 NameNode
```
URLs:
 - From hadoop 3.0.0, http://localhost:50070 was moved to http://localhost:9870. [see this](https://issues.apache.org/jira/browse/HDFS-9427?focusedCommentId=15156476&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel#comment-15156476)
 - Namenode ports: 50470 --> 9871, 50070 --> 9870, 8020 --> 9820
 -  Secondary NN ports: 50091 --> 9869, 50090 --> 9868
 - Datanode ports: 50020 --> 9867, 50010 --> 9866, 50475 --> 9865, 50075 --> 9864


Reference: - https://www.tutorialspoint.com/hadoop/hadoop_enviornment_setup.htm
