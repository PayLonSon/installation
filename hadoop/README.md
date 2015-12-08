# Hadoop 2.7.1 安裝

## 安裝環境
 OS: `Ubnutu 14.04.1LTS`
 
 先利用`ifconfig`查看所有機器的ip
 ```
 master	192.168.56.128
 node01	192.168.56.129
 node02	192.168.56.130
 ```
修改/etc/hostname

```
sudo vim /etc/hostname
sudo service hostname start
```

 安裝Java JDK
 
 ```
 sudo apt-get -y openjdk-7-jdk
 sudo ln -s /usr/lib/jvm/java-7-openjdk-amd64 /usr/lib/jvm/jdk
 ```

新增Hadoop使用者

```
sudo addgroup hadoop
sudo adduser --ingroup hadoop hduser
sudo adduser hduser sudo
su hduser
cd ~
```

建立SSH免密碼登入(以下皆為Master操作)

```
ssh-keygen -t rsa -f ~/.ssh/id_rsa -P ""
cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
scp –r ~/.ssh node01:~/
scp -r ~/.ssh node02:~/
```
下載Hadoop

```
cd ~
wget http://apache.stu.edu.tw/hadoop/common/stable2/hadoop-2.7.1.tar.gz
tar zxf hadoop-2.7.1.tar.gz
mv hadoop-2.7.1 hadoop
```
新增環境變數

`vim .bashrc`

```
export JAVA_HOME=/usr/lib/jvm/jdk/
export HADOOP_INSTALL=/home/hduser/hadoop
export PATH=$PATH:$HADOOP_INSTALL/bin
export PATH=$PATH:$HADOOP_INSTALL/sbin
export HADOOP_MAPRED_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_HOME=$HADOOP_INSTALL
export HADOOP_HDFS_HOME=$HADOOP_INSTALL
export YARN_HOME=$HADOOP_INSTALL

```
`source .bashrc`







