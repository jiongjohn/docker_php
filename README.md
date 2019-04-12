# docker下的php开发环境

基于Docker容器技术，配置一个php 和 nginx 的开发环境

## nginx环境

本实例用的是nginx-1.15.11包。 要布置环境的时候将需要安装的包下载放置在nginx目录中，如果是不同版本则需修改nginx的Dockerfile
```
ARG NV="nginx-1.15.11"
```

## php环境
本实例用的是php-5.5.17包。要布置环境的时候将需要安装的包下载放置在php目录中，如果是不同版本则需修改php的Dockerfile

```
ARG PV="php-5.5.17"
```
## 依赖
本环境的基础镜像依赖于官方的centos:6.8

## 安装

* 拉取代码
* 下载所需要安装的php和nginx安装包放在对应目录下
* 安装docker和docker-composer
* 启动环境 docker-compose up -d

