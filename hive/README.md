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

讀取.bashrc，`source .bashrc`

建立Hive所需的HDFS目錄與更改權限，`/tmp` 可能已經存在，若已經存在不須建立，但也須更改權限

```
##主要用在存放一些Hive執行過程的臨時資料
hadoop fs -mkdir /tmp 
##Hive進行管理的資料目錄
hadoop fs -mkdir /user/warehouse
hadoop fs -chmod 777 /tmp
hadoop fs -chnow 777 /user/hive/warehouse
```

安裝`libmysql-java`，用`JDBC`時需用到。

`sudo apt-get install libmysql-java`

安裝完成後，將`/usr/share/java/mysql-connector-java-5.1.28.jar`複製到`hive/lib`底下

`sudo cp /usr/share/java/mysql-connector-java-5.1.28.jar ~/hive/lib`

接著啟動MySQL，建立一個專屬Hive的帳號，啟動方式如下:

`mysql u root -p`

接著會要你輸入root密碼，輸入完後會進到`mysql>`的command模式，複製指令時不要複製到`mysql>`以及註解
```
#建立一個hive的database

mysql > create database hive; 

#建立一個MySQL使用者，帳號跟密碼都是hive，且用%代表在任何hostname都可登入

mysql> grant all on *.* to'hive'@'%' identified by 'hive';    

#更新User清單

mysql> flush privileges; 

#結束mysql

mysql> exit; #結束mysql

```



