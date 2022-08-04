---
description: gaohongbin-20220803 容器化技术第2篇（docker）
---

# lecture3 容器化技术2

1. 容器到底是什么
2. 容器Namespaces实现原理
3. 容器Cgroups实现原理

容器生态系统是由许多技术、大量专业术语和大公司相互争斗组成的

![容器技术的关系](<.gitbook/assets/截屏2022-08-03 下午7.40.37 (1).png>)

*   为什么docker出现，才引领了容器的浪潮：

    因为docker创造性地引入了“镜像”

![镜像](<.gitbook/assets/截屏2022-08-03 下午7.48.56.png>)

docker的运行模式：

![docker管理容器的模式](<.gitbook/assets/截屏2022-08-03 下午7.51.43.png>)

* 容器可以看作是一个轻量级的虚拟机，借用linux的一些隔离功能，使得应用间得以隔离

Namespace技术实际上修改了应用进程看待整个计算机的“视图”，docker容器里的应用，实际上还是宿主机上的一个进程，在宿主机的namespace下，可以看到所有容器。在单个容器的内部，只能看到自己namespace下的内容。

![namespace](<.gitbook/assets/截屏2022-08-03 下午7.55.30.png>)

* docker的网络模型， CNM（Container Network Model），最常用的是网桥的模式，帮助容器进行通信



* Cgroup

它提供了一种机制，这种机制可以根据需求把一系列任务以及子任务整合到按资源划分的组内。有了这个技术，就可以对一个进程或一组进程的计算机资源消耗进行限制。

* docker和k8s

docker完成容器的创建、部署，k8s完成容器的保持、调度、编排
