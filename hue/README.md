###Hue Install

##安裝前先安裝以下軟體，可參考`installation`其他安裝文件
```
Hadoop-2.7.1
Zookeeper-3.4.5-cdh5.4.5
HBase-1.0.0-cdh5.4.5
Hive-1.2.1
```

進到`Hive`開啟`hiveserver2`

```
bin/hiveserver2 &
```

安裝相關軟體

```
sudo apt-get install git
sudo apt-get install python2.7-dev make libkrb5-dev libxml2-dev libxslt-dev libsqlite3-dev libssl-dev libldap2-dev python-pip ant gcc g++ libkrb5-dev libmysqlclient-dev libssl-dev libsasl2-dev libsasl2-modules-gssapi-mit libsqlite3-dev libtidy-0.99-0 libxml2-dev libxslt-dev make libldap2-dev maven python-dev python-setuptools libgmp3-dev 
```


利用`git`安裝
```
git clone https://github.com/cloudera/hue.git
cd hue
make apps
build/env/bin/hue runserver
```

`cd ~`

修改Hadoop配置，`vim hadoop/etc/hadoop/hdfs-site.xml`，增加以下
```
<property>
  <name>dfs.webhdfs.enabled</name>
  <value>true</value>
</property>
```

修改Hadoop配置，`vim hadoop/etc/hadoop/cofe-site.xml`，增加以下
```
<property>
  <name>hadoop.proxyuser.hue.hosts</name>
  <value>*</value>
</property>
<property>
  <name>hadoop.proxyuser.hue.groups</name>
  <value>*</value>
</property>
```

修改Hive配置，`vim hive/conf/hive-site.xml`，搜尋並修改
```
<property>
    <name>hive.server2.authentication</name>
    <value>NOSASL</value>
  </property>
```


接下來進行Hue文件配置
```
vim desktop/conf/pseudo-distributed.ini
```

須修改的內容如下:(用搜尋修改)
```
配置項目                  值            說明
server_user               hduser
server_group              hadoop
default_hdfs_superuser    hadoop        HDFS管理用戶
