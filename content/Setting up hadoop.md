Title: Setting up hadoop in Ubuntu
date: 2017-04-02 19:23
category: Hadoop
tags: Hadoop, Blog, Environment setup
author: Harshul Jain
excerpt: This is an excerpt of my post.

***Install Java***

***Adding a dedicated hadoop system user***
```
$ sudo addgroup hadoop
$ sudo adduser --ingroup hadoop hduser
```

***configuring ssh***
```
su hduser
ssh-keygen -t rsa
cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

***Installing hadoop***
```
exit
cd /usr/local
sudo tar xzf hadoop-x.x.x.tar.gz
sudo mv hadoop-x.x.x hadoop
sudo chown -R hduser:hadoop hadoop
```

***Updating .bashrc for hduser***
```
su hduser
cd
nano .bashrc
```
put the followign contents in the .bashrc file
```
# HADOOP VARIABLES START
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
export HADOOP_HOME=/usr/local/hadoop
unalias fs &> /dev/null
alias fs="hadoop fs"
unalias hls &> /dev/null
alias hls="fs -ls"
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
# export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
# HADOOP VARIABLES END
```

```
source .bashrc
hadoop version
```

***hadoop-env.sh***
```
cd
nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh
```

comment the original JAVA_HOME line and replace it by ``export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64``.

***core-site.xml***
```
exit
sudo mkdir -p /app/hadoop/tmp
sudo chown hduser:hadoop /app/hadoop/tmp
sudo chmod 750 /app/hadoop/tmp
su hduser
cd
nano /usr/local/hadoop/etc/hadoop/core-site.xml
```
Inside the <configuration>...</configuration> tags, put the following:
```
<property>
  <name>hadoop.tmp.dir</name>
  <value>/app/hadoop/tmp</value>
  <description>A base for other temporary directories.</description>
</property>

<property>
  <name>fs.default.name</name>
  <value>hdfs://localhost:54310</value>
  <description>The name of the default file system.  A URI whose
  scheme and authority determine the FileSystem implementation.  The
  uri's scheme determines the config property (fs.SCHEME.impl) naming
  the FileSystem implementation class.  The uri's authority is used to
  determine the host, port, etc. for a filesystem.</description>
</property>
```

***mapred-site.xml***
```
nano /usr/local/hadoop/etc/hadoop/mapred-site.xml
```
Inside the <configuration>...</configuration> tags, put the following:
```
<property>
  <name>mapred.job.tracker</name>
  <value>localhost:54311</value>
  <description>The host and port that the MapReduce job tracker runs
  at.  If "local", then jobs are run in-process as a single map
  and reduce task.
  </description>
</property>

```

***hdfs-site.xml***
```
nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml
```
Inside the <configuration>...</configuration> tags, put the following:
```
<property>
  <name>dfs.replication</name>
  <value>1</value>
  <description>Default block replication.
  The actual number of replications can be specified when the file is created.
  The default is used if replication is not specified in create time.
  </description>
</property>
```

***Formatting the hdfs file system***
```
hadoop namenode -format
```

***Starting and stopping your single node cluster***
```
start-all.sh
stop-all.sh
```

