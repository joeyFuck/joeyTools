## 通用command

docker search image 搜索镜像（运行文件）（image: 镜像名称）
docker pull image (image： 镜像名称)
docker ps 查询所有启动的容器
docker ps  -a  查询所有容器
docker rm 镜像id    删除容器
docker start 镜像id   启动容器
docker stop 镜像id    停止容器

启动容器：
docker run --name master -d  -p 6379:6379 -p 26379:26379  redis
docker run 启动容器
--name 容器名称
-d 容器后台启动
-p 主机端口：容器的端口
redis 运行镜像

查看容器运行的局域网ip地址：（阿里云默认第一个启动的容器IP地址：172.17.0.2, 依次为172.17.0.3, ...）
docker inspect 容器id
docker inspect --format '{{ .NetworkSettings.IPAddress }}' 容器id

进入容器
docker exec -it  容器id bash(或者打全/bin/bash())

备份某个容器（一般用于修改某个容器后进行保存，日后可将此备份当作一个容器base进行启动）
docker commit 容器id new-container-name

docker内要安装软件的化一般需要先： apt-get update (更新依赖)

### redis:

redis-cli：自带的客户端，进入redis

$ docker exec -it 882ba4a24120 bash
root@dc416bda091c:/data# redis-cli
127.0.0.1:6379> info replication  # 显示redis信息

127.0.0.1:6379> slaveof 172.17.0.3 6379 --设置当前库为172.17.0.3 6379的从库 主库会将数据初始化同步到子库上。
127.0.0.1:6379> slaveof no one  --退出主从关系










