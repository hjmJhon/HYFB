# hyperledger 之 fabric 环境搭建(基于 Mac OS)  

### 1.安装 git(Mac 自带),vim(Mac 自带),go,curl,node,nvm,npm,docker.   
* Docker 安装见 官网 [Docker](https://www.docker.com/get-started)  
* 其他安装,自行搜索解决.

### 2.Hyperledger Fabric Samples 下载安装  
* 创建一个空目录,并进入该目录  

```
mkdir hyfa
```

```
cd hyfa
```  

* 新建文件bootstrap.sh  


```
vim bootstrap.sh  
```  

* 将https://github.com/hyperledger/fabric/blob/master/scripts/bootstrap.sh 中的内容拷贝,保存并退出  

* 赋予 bootstrap.sh 可执行权限并运行  


```
chmod +x bootstrap.sh
```  

* 配置 docker 加速器  


```
将 http://8890cb8b.m.daocloud.io 添加到如下位置
docker -> Preferences -> Deamon -> Registry mirrors.  
重启 docker  
```  

* 执行 bootstrap.sh  


```
sudo ./bootstrap.sh 1.1.0
```  

* 下载完成后, 查看相关输出内容, 如果下载有失败的镜像, 可再次执行 `$ sudo ./bootstrap.sh 1.1.0` 命令  

* 下载完成后命令行输出如下  


```
Error response from daemon: manifest for hyperledger/fabric-ca:x86_64-1.3.0 not found
Error response from daemon: No such image: hyperledger/fabric-ca:x86_64-1.3.0
===> Pulling thirdparty docker images
==> THIRDPARTY DOCKER IMAGE: couchdb

Error response from daemon: manifest for hyperledger/fabric-couchdb:x86_64-0.4.13 not found
Error response from daemon: No such image: hyperledger/fabric-couchdb:x86_64-0.4.13
==> THIRDPARTY DOCKER IMAGE: kafka

Error response from daemon: manifest for hyperledger/fabric-kafka:x86_64-0.4.13 not found
Error response from daemon: No such image: hyperledger/fabric-kafka:x86_64-0.4.13
==> THIRDPARTY DOCKER IMAGE: zookeeper

Error response from daemon: manifest for hyperledger/fabric-zookeeper:x86_64-0.4.13 not found
Error response from daemon: No such image: hyperledger/fabric-zookeeper:x86_64-0.4.13

===> List out hyperledger docker images
hyperledger/fabric-tools     latest              b7bfddf508bc        7 months ago        1.46GB
hyperledger/fabric-tools     x86_64-1.1.0        b7bfddf508bc        7 months ago        1.46GB
hyperledger/fabric-orderer   latest              ce0c810df36a        7 months ago        180MB
hyperledger/fabric-orderer   x86_64-1.1.0        ce0c810df36a        7 months ago        180MB
hyperledger/fabric-peer      latest              b023f9be0771        7 months ago        187MB
hyperledger/fabric-peer      x86_64-1.1.0        b023f9be0771        7 months ago        187MB
hyperledger/fabric-javaenv   latest              82098abb1a17        7 months ago        1.52GB
hyperledger/fabric-javaenv   x86_64-1.1.0        82098abb1a17        7 months ago        1.52GB
hyperledger/fabric-ccenv     latest              c8b4909d8d46        7 months ago        1.39GB
hyperledger/fabric-ccenv     x86_64-1.1.0        c8b4909d8d46        7 months ago        1.39GB  
```  

若出现 上面的 Error response ,说明是那几个镜像没有下载成功. 解决办法是: 
```
进入到 https://hub.docker.com/
查找 那几个失败的镜像  
命令行运行 docker pull 对应镜像  
例如 docker pull hyperledger/fabric-zookeeper
```   

* 添加环境变量  


```
export PATH=<path to download location>/bin:$PATH  
```  
注: `<path to download location>` 表示下载的 fabric-samples 文件目录所在路径  

```
例如我的 export PATH=$HOME/hyfa/fabric-samples/bin:$PATH
```



