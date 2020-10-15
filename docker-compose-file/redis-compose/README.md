# docker-compose部署Redis
## 1、参考链接
to see https://blog.csdn.net/u013652477/article/details/107833068

## 2、docker-compose.yml

```yaml
version: '3.7'

services:
  redis:
    image: redis
    container_name: redis
    hostname: redis #redis容器主机名
    restart: always
    ports:
      - 6379:6379
    networks:
      - net_db
    volumes:
      - ./conf/redis.conf:/etc/redis/redis.conf:rw #挂载redis.conf配置文件
      - ./data:/data:rw #挂载redis持久数据目录
    command:
      redis-server /etc/redis/redis.conf --appendonly yes #开启redis持久化 aof rdb
    privileged: true  #环境变量
    environment:
      - TZ=Asia/Shanghai
      - LANG=en_US.UTF-8
networks:
  net_db:
    driver: bridge

```

