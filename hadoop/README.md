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
