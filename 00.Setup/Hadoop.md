```
Java Version : 1.8.0
Hadoop Version : 3.3.2
```


## 01. Java 설치
- 설치
```
sudo apt-get update
sudo apt-get install openjdk-8-jdk
```
- 설치 확인
```
java -version
```
- 경로 설정
```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
source ~/.bashrc
```

## 02. Hadoop 설치
### 다운로드
```
wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.2/hadoop-3.3.2.tar.gz
tar zxvf hadoop-3.3.2.tar.gz
```

### 기본 설정
```
# hadoop
export HADOOP_HOME=/path/to/hadoop-3.3.2
# path
export PATH=$PATH:$HADOOP_HOME/bin
# 적용
source ~/.bashrc
```
xml 파일들은 etc/hadoop 내애 존재함  
- core-site.xml
```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```
- Namenode, Datanode directory 생성
```
mkdir -p hadoop-3.3.2/dfs/data
mkdir -p hadoop-3.3.2/dfs/name
```
- hdfs-site.xml
```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/home/fastcampus/hadoop-3.3.2/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/home/fastcampus/hadoop-3.3.2/dfs/data</value>
    </property>
</configuration>
```
- mapred-site.xml
```
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.application.classpath</name>
        <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
    </property>
</configuration>
```
- yarn-site.xml
```
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.env-whitelist</name>
        <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_HOME,PATH,LANG,TZ,HADOOP_MAPRED_HOME</value>
    </property>
</configuration>
```
- hadoop-env.sh
```
# JAVA_HOME 추가
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```

## 03. HDFS 실행
```
hdfs namenode -format
sbin/start-dfs.sh
http://localhost:9870
```

## 04. YARN 실행
```
sbin/start-yarn.sh
http://localhost:8088/
```


