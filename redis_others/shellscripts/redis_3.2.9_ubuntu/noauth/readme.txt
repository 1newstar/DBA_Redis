﻿脚本使用说明
1. 该脚本由多个功能不同的小脚本组成
2. ubuntu系列搭建redis3.2.9版本的主从_sentinel_consul高可用，实现自动故障转移。
3. 小脚本可单独使用，例如redis单实例安装
4. 具体执行如下：


将脚本传到 /root/家目录下
#安装
bash RedisInstall.sh 
#启动redis服务
./redisctl redis start 6379
./redisctl redis start 6380
#启动sentinel服务
./redisctl sentinel start 26379
#查看进程
ps -ef|grep redi[s]
#启动consul服务
nohup /bin/consul agent -dev  -config-dir=/alidata/consul/conf &> /alidata/consul/consul.log &
#查看consul进程
ps -ef|grep consul
# 测试
dig redis.service.consul

# 测试整体架构
redis-cli -h redis.service.consul -p 6379 -a zyadmin info replication
