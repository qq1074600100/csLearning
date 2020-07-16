# Kubernetes(K8s)



## 起源

borg --> k8s

Google采用go语言开发



## 特点

1. 轻量级：资源消耗少
2. 开源
3. 弹性伸缩：便于升级、便于资源释放
4. 负载均衡：IPVS架构



## 介绍说明

### 要点

1. 框架
2. 组件
3. 名词解释

### 整体架构

![image-20200715170424883](C:\Users\maplezhao\AppData\Roaming\Typora\typora-user-images\image-20200715170424883.png)

![image-20200715171521123](C:\Users\maplezhao\AppData\Roaming\Typora\typora-user-images\image-20200715171521123.png)

### 组件

1. APISERVER：所有服务访问统一入口
2. ReplicationController：维持副本期望数
3. Scheduler：调度器，接受任务，选择合适节点分配任务
4. etcd：键值对存储，内存或数据库，储存K8S重要信息
5. Kubelet：直接跟容器引擎（Docker）交互，管理容器生命周期
6. Kube-proxy：实现访问映射

### 插件

1. CoreDNS：为集群SVC创建域名IP映射
2. DashBoard：给集群提供B/S访问
3. IngressController：四层代理提升为七层代理
4. Federation：跨集群统一管理
5. Prometheus：集群监控能力
6. ELK：集群日志统一分析接入平台



## 基础概念

### 要点

1. 什么是Pod：最小的封装集合
2. 控制器类型
3. 网络通讯模式

### Pod

#### 分类

- 自主式
- 控制器管理式

#### 概念

- 每个Pod会有一个pause容器
- 每个Pod管理多个容器，并且共享IP和存储，端口号不可重复
- 多个容器类似于一个容器中的进程

### 控制器类型

#### RC&RS&Deployment>HPA

- ReplicationController：保持副本数与用户定义一致
- ReplicaSet：与RC一样，增加了对selector的支持
- Deployment：RS可以独立使用，但用deployment自动管理RS，可以避免不兼容问题
- Horizontal Pod Autoscaling：适用于Deployment和ReplicaSet，支持根据CPU利用率自动扩缩容

#### StatefulSet

- 目的：解决有状态服务问题
- 应用场景：
  - 持久化存储一致
  - 稳定的网络标志，即域名不变
  - 有序部署
  - 有序收缩、删除

#### DaemonSet

- 目的：

#### Job， Cronjob











## K8s安装

### 要点

1. 集群构建



## 资源清单

### 要点

1. 什么是资源？
2. 资源清单语法
3. 编写Pod
4. **Pod生命周期**



## Pod控制器（重点）

### 要点

1. 各种控制器的使用及特点



## 服务发现

### 要点

1. 掌握SVC原理及构建方式



## 存储

### 要点

1. 掌握各存储类型的特点
2. 能选择合适的存储方案



## 调度器

### 要点

1. 掌握调度器原理
2. 能根据需求把Pod放在合适的节点



## 集群安全机制

### 要点

1. 集群的认证、鉴权
2. 访问控制原理及流程



## HELM

### 要点

1. 类似于linux yum
2. HELM原理
3. HELM模板自定义
4. HELM部署常用插件



## 运维

### 要点

1. Kubeadm源码修改
2. Kubernetes高可用构建