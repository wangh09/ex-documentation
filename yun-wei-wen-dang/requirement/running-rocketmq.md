# Rocketmq {#toc_0}

This guide will tell us how to install rocketmq and create topic

### 1、Prerequisite {#toc_1}

The following softwares are assumed installed:

1. 64bit OS, Linux/Unix/Mac is recommended;
2. 64bit JDK 1.8+;
3. Maven 3.2.x
4. Git

### 2、Install Rocketmq {#toc_2}

Click [here](https://www.apache.org/dyn/closer.cgi?path=rocketmq/4.3.0/rocketmq-all-4.3.0-source-release.zip) to download the 4.3.0 source release. Also you could download a binary release from [here](http://rocketmq.apache.org/release_notes/release-notes-4.3.0/).

Now execute the following commands to unpack 4.3.0 source release and build the binary artifact.

```
unzip rocketmq-all-4.3.0-source-release.zip
cd rocketmq-all-4.3.0/
mvn -Prelease-all -DskipTests clean install -U
cd distribution/target/apache-rocketmq
```

### 3、Start {#toc_3}

* 3.1 Start Name Server

```
nohup sh bin/mqnamesrv &
tail -f ~/logs/rocketmqlogs/namesrv.log
The Name Server boot success...
```

* 3.2 Start Broker

```
nohup sh bin/mqbroker -n localhost:9876 autoCreateTopicEnable=true &
tail -f ~/logs/rocketmqlogs/broker.log 
The broker[%s, 10.146.0.7:10911] boot success...
```

### 4、Start failure\(Non-required operation\) {#toc_4}

Usually successful startup after the above steps, but sometimes overflow errors occur。You need to change the size of Xms, Xmx, Xmn in runserver.sh and runbroker.sh.

```
vim bin/runserver.sh
AVA_OPT="${JAVA_OPT} -server -Xms1g -Xmx1g -Xmn512m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m"
vim bin/runbroker.sh
JAVA_OPT="${JAVA_OPT} -server -Xms1g -Xmx1g -Xmn512m"
```

### 5、Create Topic {#toc_5}

```
.bin/mqadmin updateTopic -c DefaultCluster -n localhost:9876 -t q_order_to_seq -r 1 -w 1 -o true
.bin/mqadmin updateTopic -c DefaultCluster -n localhost:9876 -t q_seq_to_match -r 1 -w 1 -o true
.bin/mqadmin updateTopic -c DefaultCluster -n localhost:9876 -t q_match_to_clearing -r 10 -w 10 -o true
.bin/mqadmin updateTopic -c DefaultCluster -n localhost:9876 -t q_clearing_to_account -r 10 -w 10 -o true
.bin/mqadmin updateTopic -c DefaultCluster -n localhost:9876 -t q_match_quotation -r 1 -w 1 -o true
.bin/mqadmin updateTopic -c DefaultCluster -n localhost:9876 -t q_post_order -r 10 -w 10 -o true
```

### 6、Display the Topic {#toc_6}

```
.bin/mqadmin topicList -n localhost:9876
```



