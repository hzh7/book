# Docker

## 安装
> https://docs.docker.com/get-docker/

### 镜像加速器
```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
"registry-mirrors": ["https://la9r8dia.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 一些命令
- 启动服务  
  sudo systemctl start docker
- 创建容器  
  sudo docker run --runtime=nvidia -p 5592:5592 -p 5593:5593 -p 8899:8888 -p 8022:22 --name="hzh_tf" -v ~/workspace/hzh/remote_workspace:/workspace/hzh/remote_workspace -it tensorflow/tensorflow:1.14.0-gpu-py3 /bin/bash
- 启动容器   
  sudo docker start hzh_tf
- 进入容器   
  sudo docker attach hzh_tf
  docker exec -it mysql /bin/bash
- 退出不关闭容器  
  Ctrl + P + Q
- 重启ssh服务   
  service ssh restart
- 远程登陆  
  ssh root@59.78.194.131 -p 8022 / 1234
- 重启应用  
  docker restart redis

## 常用容器
### docker里启动mysql

    sudo docker run -p 3306:3306 --name mysql -v /mydata/mysql/log:/var/log/mysql -v /mydata/mysql/data:/var/lib/mysql -v /mydata/mysql/conf:/etc/ mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7

  [Docker安装Mysql5.7](https://www.hellojava.com/a/86680.html)

### docker redis

    docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data -v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf -d redis redis-server /etc/redis/redis.conf

### TensorFlow1.12容器
    docker run --runtime=nvidia -it --rm tensorflow/tensorflow:1.12.0-gpu-py3

    sudo docker run --runtime=nvidia -p 5592:5592 -p 5593:5593 -p 8899:8888 -p 8022:22 --name="hzh_tf" -v ~/workspace/hzh/remote_workspace:/workspace/hzh/remote_workspace -it tensorflow/tensorflow:1.14.0-gpu-py3 /bin/bash


## 搭建tf环境

### 相关参考
[PyCharm+Docker：打造最舒适的深度学习炼丹炉](https://zhuanlan.zhihu.com/p/52827335)
[Docker 退出容器但不关闭当前容器](https://blog.csdn.net/LEoe_/article/details/78685186)
[查看tensorflow是否支持GPU，以及测试程序](https://blog.csdn.net/renhaofan/article/details/81987728)

### 注意点
- [PyCharm+Docker：打造最舒适的深度学习炼丹炉](https://zhuanlan.zhihu.com/p/52827335)中提到的配置ssh，可能还是有问题，需要vim进入到`/etc/ssh/sshd_config`将`PermitRootLogin yes`的注释去掉，才可以远程ssh登陆上去。

- 用`lsb_release -a`查看可以知道其实该容器本质是个Ubuntu18.04
