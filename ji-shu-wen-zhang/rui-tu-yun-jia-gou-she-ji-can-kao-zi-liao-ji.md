# 锐途云架构设计参考资料集

## 锐途云架构设计参考资料集

本文尝试收集关于云原生+微服务架构的一系列文章，并梳理出一套现阶段最可行的架构方式。

## Overview

#### 设计思想

* 核心能力通用化
* 基础架构容器化
* 应用架构微服务化
* 业务架构中台化
* 开发/交付流程自动化

#### 理论基础

* [容器十年 ——一部软件交付编年史](https://yq.aliyun.com/articles/707171?spm=a2c4e.11153940.0.0.59463a8au2HrCv)

PaaS -&gt; 云原生 CloudNative

#### 基础架构

* Python Flask
* Flask Micoservices
* Gitlab CI
* Docker
* Kubernetes

## 工具

#### 项目管理工具

* [https://arrwayworkspace.slack.com/messages/CLDKJ6ZU5/](https://github.com/georgezouq/blog/tree/d050dec81656b3f09f692730b8cb487521c94aa0/Arrway%20Slack/README.md)

#### Docker 基础

* [How To Build and Deploy a Flask Application Using Docker on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-build-and-deploy-a-flask-application-using-docker-on-ubuntu-18-04)

#### Python Micoservics

* [TDD开发容器化的Python微服务应用](https://www.qikqiak.com/post/tdd-develop-python-microservice-app/)
* [上文原始文章：](https://realpython.com/tdd/)
* [Microservices with Docker, Flask, and React](https://testdriven.io/courses/microservices-with-docker-flask-and-react/part-one-microservices/)

**Python 环境管理工具 pyenv-virtualenv**

```text
pyenv-virtualenv 是pyenv的插件，为pyenv设置的python版本提供隔离的虚拟环境，设置虚拟环境后，在当前目录下面安装的第三方库都不会影响其他环境
```

```text
brew update
brew install pyenv

brew install pyenv-virtualenv
```

[Mac下pyenv与pyenv-virtualenv的安装和使用 ](https://github.com/eteplus/blog/issues/4)

安装 Pyenv 的 Python 3.6.4 版本

```text
pyenv install 3.6.4
```

## Kubernetes 集群

#### 资料集

* [Kubernetes Handbook](https://jimmysong.io/kubernetes-handbook/)
* [2019最新k8s集群搭建教程 \(centos k8s 搭建\)](https://juejin.im/post/5cb7dde9f265da034d2a0dba#heading-2)
* [简单的 Kubernetes 集群搭建](https://juejin.im/post/5bb45d63f265da0a9e532128)
* [谈 Kubernetes 的架构设计与实现原理](https://draveness.me/understanding-kubernetes)

### 阿里云容器服务 - Kubernetes 版本

#### 一、创建集群

特别简单 下一步下一步就行

* [部署 Serving Hello World 应用示例](https://help.aliyun.com/document_detail/121534.html?spm=5176.2020520152.0.0.49fd16ddlDTRtj)

#### 二、[通过 kubectl 连接 Kubernetes 集群](https://help.aliyun.com/document_detail/86494.html?spm=a2c4g.11186623.2.12.4afe1facKpVrhu#task-ubf-lhg-vdb)

#### 应用部署

* [带你理解Kubernetes，部署一个Node应用](https://segmentfault.com/a/1190000014116698)
* [镜像创建无状态Deployment应用](https://help.aliyun.com/document_detail/87784.html?spm=a2c4g.11186623.6.627.1f7d7a691cLPyw)
* [Deploy Vue.js Application use Docker, Kubernetes on AWS EKS.](https://medium.com/@thanhtungvo/deploy-vue-js-application-use-docker-kubernet-on-aws-eks-3b1b38fcbef3)
* [Dockerize Vue.js App](https://vuejs.org/v2/cookbook/dockerize-vuejs-app.html)

#### 三、[Gitlab CI 与 Kubernetes结合](https://www.qikqiak.com/post/gitlab-ci-k8s-cluster-feature/)

### 最佳实践

* [五大Kubernetes最佳实践](https://cloud.tencent.com/developer/article/1151963)
* [从Docker到Kubernetes进阶](https://www.qikqiak.com/k8s-book/docs/14.Kubernetes%E5%88%9D%E4%BD%93%E9%AA%8C.html)

#### Helm

* [使用Helm部署微服务应用](https://help.aliyun.com/document_detail/85935.html?spm=5176.10695662.1996646101.searchclickresult.59d416b1r2vrUz)

#### Gitlab CI

* [使用GitLab CI在Kubernetes服务上运行GitLab Runner并执行Pipeline](https://help.aliyun.com/document_detail/106968.html?spm=5176.10695662.1996646101.searchclickresult.3ec9e56fEm0Fwv)

### 问题

* [教程](https://www.servicemesher.com/blog/kubernetes-crd-quick-start/)
* [Kubernetes 部署失败的 10 个最普遍原因（Part 1）](http://dockone.io/article/2247)
* [GitLab + Kubernetes + Google Cloud Platform](https://medium.com/@vitalypanukhin/gitlab-kubernetes-gcp-6d3ce7349dce)
* [Kubernetes 如何支持私有镜像](https://help.aliyun.com/document_detail/86562.html)

### 工具

* [阿里云镜像控制台](https://cr.console.aliyun.com/cn-hangzhou/instances/repositories)

