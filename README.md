# Hadoop-installation
Hadoop installation steps in mac 

## 1. Install Hadoop 3.0.0
## 2. Cd to Hadoop Folder to configure hadoop environment. Configuration files locations In linux: /usr/local/Cellar/hadoop/3.0.0/libexec/etc/hadoop
### 1. Open hadoop-env.sh and comment out below line
   #export HADOOP_OPTS="-Djava.net.preferIPv4Stack=true -Dsun.security.krb5.debug=true -Dsun.security.spnego.debug"

### 2. Open core-site.xml and add below data:
<configuration>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/usr/local/Cellar/hadoop/hdfs/tmp</value>
    <description> A base for other temporary directories. </description>
  </property>
  <property>
    <name>fs.default.name</name>
    <value>hdfs://localhost:9000</value>
  </property>
</configuration>
### 3. Open hdfs-site.xml and add below data:
<configuration>

  <property>
   <name>dfs.replication</name>
   <value>1</value>
   <description> How many copies of data our hadoop will have. Value defines how many copies </description>
  </property>

</configuration>
### 4. Open marred-site.xml and add below data:
<configuration>
  <property>
    <name>mapred.job.tracker</name>
    <value>localhost:9010</value>
    <description> Mapreduce - maps the data and reduces that data to give it to you. This is done by deamon. This tracks all jobs running in hadoop cluster. </description>
   </property>
</configuration>
### 5. Below commands to start or stop the hadoop. 
alias hstart = '/usr/local/Cellar/hadoop/3.0.0/sbin/start-dfs.sh'
alias hstop = '/usr/local/Cellar/hadoop/3.0.0/sbin/stop-dfs.sh'


Note: If u get error like permission denied at sept5, create a ssh key with no password!! 


Output after succesful hadoop installation looks like below:

krishnas-mbp:sbin krishna.damarla$ ./start-dfs.sh 
Starting namenodes on [localhost]
Starting datanodes
Starting secondary namenodes [krishnas-mbp.widas.de]
2018-04-10 14:14:40,129 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

(Late message is just a warning. Can be neglected) 
