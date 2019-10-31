## 通用command

1. docker search image 搜索镜像（运行文件）（image: 镜像名称）
2. docker pull image (image： 镜像名称)
3. docker ps 查询所有启动的容器
4. docker ps  -a  查询所有容器
5. docker rm 镜像id    删除容器
6. docker start 镜像id   启动容器
7. docker stop 镜像id    停止容器

8. 启动容器：docker run --name master -d  -p 6379:6379 -p 26379:26379  redis
 
  docker run 启动容器
  --name 容器名称
  -d 容器后台启动
  -p 主机端口：容器的端口
  redis 运行镜像

9. 查看容器运行的局域网ip地址：（阿里云默认第一个启动的容器IP地址：172.17.0.2, 依次为172.17.0.3, ...）

  docker inspect 容器id
  docker inspect --format '{{ .NetworkSettings.IPAddress }}' 容器id

10. 进入容器 docker exec -it  容器id bash(或者打全/bin/bash())

11. 备份某个容器（一般用于修改某个容器后进行保存，日后可将此备份当作一个容器base进行启动）

  docker commit 容器id new-container-name

12. docker内要安装软件的化一般需要先： apt-get update (更新依赖)

### redis:

1. redis-cli：自带的客户端，进入redis
1. redis-cli -h 192.168.154.128 -p 6379 # 指定进入哪个实例 默认为localhost:6379

2. $ docker exec -it 882ba4a24120 bash
3. root@dc416bda091c:/data# redis-cli
4. 127.0.0.1:6379> info replication  # 显示redis信息
5. redis-cli info replication #查看redis的复制授权信息
6. redis-cli info sentinel   #查看redis的哨兵信息

7. 127.0.0.1:6379> slaveof 172.17.0.3 6379 --设置当前库为172.17.0.3 6379的从库 主库会将数据初始化同步到子库上。
8. 127.0.0.1:6379> slaveof no one  --退出主从关系

9. 启动redis,进到redis-servcer所在文件夹， ./redis-server   redis.conf
10. 进到redis-cli所在文件夹> ./redis-cli  连接到redis，就可以使用redis-cli提供的命令了









