# Docker



#### 什么是Docker？

```
Docker是一个容器化平台，它以容器的形式将您的应用程序及其所有依赖项打包在一起，以确保您的应用程序在任何环境中无缝运行。
```

####  

#### CI（持续集成）服务器的功能是什么？

```
CI功能就是在每次提交之后不断地集成所有提交到存储库的代码，并编译检查错误
```

 

#### 什么是Docker镜像？

```
Docker镜像是Docker容器的源代码，Docker镜像用于创建容器。使用build命令创建镜像
```

 

#### 什么是Docker容器？

```
Docker容器包括应用程序及其所有依赖项，作为操作系统的独立进程运行
```

 

#### Docker容器有几种状态？

```
Docker容器可以有四种状态：
运行
已暂停
重新启动
已退出
```

 

#### Docker使用流程

```
1）创建Dockerfile后，您可以构建它以创建容器的镜像
2）推送或拉取镜像。
```

 

#### Dockerfile中最常见的指令是什么？

```
Dockerfile中的一些常用指令如下：
FROM：指定基础镜像
LABEL：功能是为镜像指定标签
RUN：运行指定的命令
CMD：容器启动时要运行的命令
```

 

#### Dockerfile中的命令COPY和ADD命令有什么区别？

```
COPY与ADD的区别COPY的<src>只能是本地文件，其他用法一致
```

 

#### docker常用命令？

```
docker pull    拉取或者更新指定镜像
docker push     将镜像推送至远程仓库
docker rm    删除容器
docker rmi    删除镜像
docker images    列出所有镜像
docker ps    列出所有容器
```



