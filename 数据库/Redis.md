# Redis

## 搭建Redis集群
[Redis 集群搭建](https://juejin.im/post/6844904062295474189)

遇到的一个坑：修改配置文件后直接使用redis-serve加载配置文件不会生效，需要用redis-cli进入后使用shutdown关闭，然后重新开启服务才会生效。也许是和redis的安装方式有关，这里用的是上面博客里写的源码编译安装。