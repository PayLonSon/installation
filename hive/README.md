###Hive Install

### 版本，以下安裝皆是在hduser這個使用者底下，請先確定所有機器皆有hduser或同Hadoop的user

```
Ubuntu 14.04
Hadoop-2.7.1
hive-1.2.1
```

##將Hive安裝於Master(切記注意使用者須切換至同Hadoop使用者)

`sudo wget http://apache.stu.edu.tw/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz`

解壓縮 : `tar -zxvf apache-hive-1.2.1-bin.tar.gz`

更名 : 　`mv apache-hive-1.2.1-bin/ hive`

在`.bashrc`增加Hive環境變數

````
vim .bashrc
  export HIVE_HOME=/home/hduser/hive
  export PATH=$HIVE_HOME/bin:$HIVE_HOME/conf:$PATH
  ```
