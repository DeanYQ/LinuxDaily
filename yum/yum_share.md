# Yum Share

## Change the Mirror source from default to Aliyun source

wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

## Command

* yum -C search

Search the package from the local machine. Don't need search the software information through Internet.

* yum makecache

create the pakcage information from remote server and cache it in the local machine to speed up the software search.

* yum clean all

remove all the data assocated with the all the containers.

## Others

### What's the EPEL

EPEL is a software source of yum. It contains a lot of software that not included int he basic source.
You can try install the EPEL source by 
$ yum install http://mirrors.hustunique.com/epel//6/x86_64/epel-release-6-8.noarch.rpm


### Install aria2c on Centos7

  yum install epel-release -y
  yum install aria2 -y
