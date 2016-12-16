# Docker 安装 Nginx

## 方法一: 通过 Dockerfile 构建

### 创建 Dockerfile(经常需要fq才可以呀)

> 参考[docker-nginx](https://github.com/nginxinc/docker-nginx/blob/master/stable/jessie/Dockerfile#L4)

- 首先, 创建目录nginx, 用于存放后面的相关东西。

```shell
ly@ubuntu:~/ly$ mkdir -p ~/nginx/www ~/nginx/logs ~/nginx/conf
```

www目录将映射为nginx容器配置的虚拟目录
logs目录将映射为nginx容器的日志目录
conf目录里的配置文件将映射为nginx容器的配置文件

进入创建的nginx目录, 创建 Dockerfile

```Dockerfile

```

通过 `Dockerfile` 创建一个镜像, 替换成你自己的名字

```shell
docker build -t ly/nginx:1.10 .
```

#### 运行容器

- 简单运行

```shell
docker run -p 80:80 --name ly-nginx4 -d ly/nginx:1.10
```
命令说明:

`-p 80:80`: 将容器的80端口映射到主机的 80 端口上

`--name ly-nginx4`: 将容器命名为 ly-nginx4

`-v $PWD/www:/www`：将主机中当前目录下的www挂载到容器的/www

`-v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf`：将主机中当前目录下的nginx.conf挂载到容器的/etc/nginx/nginx.conf

`-v $PWD/logs:/wwwlogs`：将主机中当前目录下的logs挂载到容器的/wwwlogs


- 映射(挂载文件夹)文件夹这种方式暂时运行不成功
```shell
ly@ubuntu:~/ly$ docker run -p 80:80 --name ly-nginx -v $PWD/nginx/www:/usr/share/nginx/html -v $PWD/nginx/conf/nginx.conf:/etc/nginx/conf.d/default.conf -v $PWD/nginx/logs:/var/log/nginx -d ly/nginx:1.10
```

## 方法二: docker pull nginx

查找 Docker Hub 上的 nginx 镜像

```shell
ly@ubuntu:~/ly$ docker search nginx
```

推荐拉取官方的镜像

```shell
$ docker pull nginx
```

等下载完成后, 我们就可以在本地镜像列表里查到 REPOSITORY 为 nginx 的镜像了

### 使用 nginx 镜像

#### 运行容器

- 简单运行

```shell
docker run -p 80:80 --name ly-nginx4 -d ly/nginx:1.10
```
命令说明:

`-p 80:80`: 将容器的80端口映射到主机的 80 端口上

`--name ly-nginx4`: 将容器命名为 ly-nginx4

`-v $PWD/www:/www`：将主机中当前目录下的www挂载到容器的/www

`-v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf`：将主机中当前目录下的nginx.conf挂载到容器的/etc/nginx/nginx.conf

`-v $PWD/logs:/wwwlogs`：将主机中当前目录下的logs挂载到容器的/wwwlogs


- 映射(挂载文件夹)文件夹这种方式暂时运行不成功

```shell
ly@ubuntu:~/ly$ docker run -p 80:80 --name ly-nginx -v $PWD/nginx/www:/www -v $PWD/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v $PWD/nginx/logs:/wwwlogs -d nginx
```