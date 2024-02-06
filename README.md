# dps（基于 shell 的 docker ps 增强）

## 概述

实现批量或选定 docker 容器导出其启动命令

## 安装

```bash
curl -o /usr/local/bin/dps https://raw.githubusercontent.com/wangrui027/dps/master/dps
chmod +x /usr/local/bin/dps
dps
```

程序依赖 `jq` 及 `docker`，请提前安装

jq: [https://jqlang.github.io/jq/](https://jqlang.github.io/jq/)

docker: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

## 使用

选定导出：

```bash
[root@vm-centos7 ~]# dps

================ 本程序负责批量或选定 docker 容器导出其启动命令 Powered by 王睿 ================
支持导出的启动参数如下：
[-d, -P, -p, -v, -e, -m, -u, -w, --name, --restart, --entrypoint, --privileged]
======================
选定导出：dps
批量导出：dps -a
======================
ref: https://docs.docker.com/engine/reference/commandline/container_run/
================================================================================================

INDEX   CONTAINER ID   NAMES   IMAGE
1       a3b3845260e7   nginx   nginx

请输入导出启动命令的的容器序号或容器名称：1

docker run -dP \
 --name nginx \
 --restart on-failure:2 \
 -v "/opt/wangrui/:/opt/wangrui" \
 -e "name=wangrui" \
 -p 8081:80/tcp \
 -w /opt \
 nginx
```

批量导出：

```bash
[root@vm-centos7 ~]# dps -a

所用容器启动命令已保存至 dps_1707192678213.txt 文件

[root@vm-centos7 ~]# cat dps_1707192678213.txt 
docker run -dP \
 --name nginx \
 --restart on-failure:2 \
 -v "/opt/wangrui/:/opt/wangrui" \
 -e "name=wangrui" \
 -p 8081:80/tcp \
 -w /opt \
 nginx
```
