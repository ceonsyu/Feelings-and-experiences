# 核心概念
## Pod
最小的调度和资源单元
## volume
是抽象的存储概念，管理pod等需要的文件资源
## deployment
是Pod之上的抽象，定义了一组Pod和Pod版本的副本数量
## service
一项服务为一个或多个pod实例提供静态IP地址
## namespace
用于在集群内实现逻辑隔离
## kubectl
命令行工具
## 学习工具
minikube
kubernetes dashboard
## Pod和Service深入理解
pod天生的为其成员容器提供了**网络**和**存储**两种资源

探针probe，对容器进行定期诊断。

service 是将运行在一组pod上的应用程序公开为网络服务的抽象方法，服务发现、负载均衡等。
## 运行机制
![运行机制](../figures/截屏2022-08-05%20下午3.49.10.png)
