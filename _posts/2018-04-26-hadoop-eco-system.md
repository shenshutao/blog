---
layout: splash
title: "在DigitalOcean上 搭建Hadoop系统"
date:   2018-04-26 18:06:47 +0800
categories: machine learning
comments: true
share: true
published: true
---
* 目录    
{:toc}

## 前言
- 学习笔记，如果用到生产环境请注意安全配置。
- 因为DigitalOcean比较便宜，所以选择这个平台。    
- 本人用Mac操作系统。  
- 前面几步也可以看[这个Youtube上的视频](https://youtu.be/HT_3F6TGiZY)

## 准备SSH Key
- 准备ssh的key，在自己机器上执行以下操作，[网站链接](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets)。  

## 买四台主机，主机名和配置如下
![servers]({{ site.baseurl }}/img/do_servers.png){:width="200px"}

## IP抄下来    
```
159.65.135.11 hadoop-01.bde.com hadoop-01
206.189.36.21 hadoop-02.bde.com hadoop-02
206.189.42.80 hadoop-03.bde.com hadoop-03
206.189.40.146 hadoop-04.bde.com hadoop-04
```

## 前期配置
四台机器都需要配置一下，自己机器上的hosts文件也改一下方便用浏览器：
```
ssh root@hadoop-01.bde.com
# Config Host
vi /etc/hosts
	# remove the self point ...
	# add the above IP Hostname mapping.
	# 配置完长下面这样：
		# The following lines are desirable for IPv4 capable hosts
		127.0.0.1 localhost.localdomain localhost
		127.0.0.1 localhost4.localdomain4 localhost4

		# The following lines are desirable for IPv6 capable hosts
		::1 localhost.localdomain localhost
		::1 localhost6.localdomain6 localhost6

		159.65.135.11 hadoop-01.bde.com hadoop-01
		206.189.36.21 hadoop-02.bde.com hadoop-02
		206.189.42.80 hadoop-03.bde.com hadoop-03
		206.189.40.146 hadoop-04.bde.com hadoop-04

vi /etc/selinux/config
	SELINUX=disabled

reboot
ssh root@hadoop-02.bde.com
...
ssh root@hadoop-03.bde.com
...
ssh root@hadoop-04.bde.com
...
vi /etc/hosts
```

## 安装CDH (Cloudera Distribution Including Apache Hadoop)
```
ssh root@hadoop-01.bde.com
yum install wget
wget http://archive.cloudera.com/cm5/installer/latest/cloudera-manager-installer.bin
chmod +x cloudera-manager-installer.bin 
./cloudera-manager-installer.bin 
# 一路点Accept就好了
```

## 配置CDH
装好以后等一会儿，让他启动，用浏览器进入网址： http://hadoop-01.bde.com:7180/    
admin/admin 登陆    
基本上默认配置特别的几个：    
- Specify hosts for your CDH cluster installation.
```
hadoop-0[1-4].bde.com
```
- Provide Login Credentials
使用我们刚才建立的ssh key。

- Select Services
我选了 Core with Spark， 你也可以选别的

@@@ 好了，初步搞定了，现在是Spark1，需要Spark2的话继续往下配
--------------------------
## 安装java8 和 spark2
安装java8，[官方攻略](https://www.cloudera.com/documentation/enterprise/latest/topics/cdh_cm_upgrading_to_jdk8.html#xd_583c10bfdbd326ba-590cb1d1-149e9ca9886--7c46)   
```
1. 在7180，停止Cluster全部服务
2. 在7180，停止Cloudera Management Service
3. Hadoop-01终端： 
	service cloudera-scm-agent stop
	service cloudera-scm-server stop
4. 然后在四个机器上：
	yum install wget
	cd /usr/java
	wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u171-b11/512cd62ec5174c3487ac17c61aaa89e8/jdk-8u171-linux-x64.tar.gz"
	tar xzf jdk-8u171-linux-x64.tar.gz
	rm -rf jdk-8u171-linux-x64.tar.gz
5. Hadoop-01终端：
	vi /etc/default/cloudera-scm-server
	在开头加上
	export JAVA_HOME=/usr/java/jdk1.8.0_171
	service cloudera-scm-server start
	service cloudera-scm-agent start
6. 等它启动，在7180，Hosts -> configure -> Java Home Directory, 填 /usr/java/jdk1.8.0_171
7. 在7180，启动Cluster全部服务
8. 在7180，启动Cloudera Management Service
```

## 安装spark2，[官方攻略](https://www.cloudera.com/documentation/spark2/latest/topics/spark2_installing.html)
```
cd
wget http://archive.cloudera.com/spark2/csd/SPARK2_ON_YARN-2.3.0.cloudera2.jar
mv SPARK2_ON_YARN-2.3.0.cloudera2.jar /opt/cloudera/csd
chmod 644 /opt/cloudera/csd/SPARK2_ON_YARN-2.3.0.cloudera2.jar
service cloudera-scm-server restart

等7180重启，在它右上角有个包裹形状的按钮，点击。可以在列表里面看见spark2，点击download-Distribute-Active。
建议点掉上面configuration里面的 Validate Parcel Relations。
重启整个cluster
在7180，Add service -> Spark2， 依赖YARN就好。
History server选hadoop-01， gateway全部选中，按继续。
在7180，停止spark，移去spark，两个都选None。
在7180，点YARN - configuration - 搜 Container Memory
	把yarn.nodemanager.resource.memory-mb设成1.5GB
	把yarn.scheduler.maximum-allocation-mb也设成1.5GB
	分发该配置，点击上方电源图标右边那个按钮 
Hadoop-01终端： 
	mkdir /var/log/spark2/lineage
	chmod 777 /var/log/spark2/lineage
	（这个好像是2.3才有的功能，还没找到怎样disable它，先简单处理...）
```

## 小试spark2
```
1. 切换hdfs用户
	su hdfs
	cd
2. 放个文件上去
	vi purplecow.txt 写几行
	hadoop fs -put purplecow.txt .
3. 尝试运行spark2-shell
	export JAVA_HOME=/usr/java/jdk1.8.0_171
	spark2-shell
	>>  sc.textFile("purplecow.txt").count()
4. 尝试运行pyspark2
	JAVA_HOME=/usr/java/jdk1.8.0_171 pyspark2
	>> sc.textFile("purplecow.txt").count()
5. 退出
	Control + D
	exit
```

@@@ 只用Scala的话，下面的就不用配置了
--------------------------
## 安装pyspark + juptyer notebook
```
python --version
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
yum install python-devel
yum groupinstall "Development tools"
pip install jupyter
pip install findspark
```

## 运行jupyter
```
export PYSPARK_PYTHON=/usr/bin/python
export HADOOP_USER_NAME=hdfs
export SPARK_HOME=/opt/cloudera/parcels/SPARK2-2.3.0.cloudera2-1.cdh5.13.3.p0.316101/lib/spark2 
export JAVA_HOME=/usr/java/jdk1.8.0_171 
jupyter notebook --ip=159.65.135.11 --port=80 --allow-root &
```

## 小试jupyter,[例子1](https://creativedata.atlassian.net/wiki/spaces/SAP/pages/82254081/Pyspark+-+Read+Write+files+from+HDFS), [例子2](https://spark.apache.org/docs/2.1.0/sql-programming-guide.html#loading-data-programmatically)
```
import findspark
findspark.init()
from pyspark.sql import SparkSession

sparkSession = SparkSession.builder.appName("example-pyspark-read-and-write").getOrCreate()
data = [('First', 1), ('Second', 2), ('Third', 3), ('Fourth', 4), ('Fifth', 5)]
df = sparkSession.createDataFrame(data)

# Write into HDFS
df.write.csv("example.csv")

# Read from HDFS
df_load = sparkSession.read.csv('example.csv')
df_load.show()
```

## 安全起见，备份一下吧... 
在DigitalOcean账户下，Image，创建Snapshot。

## 配置完成




