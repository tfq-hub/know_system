## Kubernetes常用命令

查看集群版本

```
kubectl version
```

集群诊断

```
kubectl get componentstatuses
```

controller-manager 负责运行各种控制器来校正集群的行为，确保服务的所有副本都是可用的和健康的；
etcd服务器是一个存储系统，供集群存放所有的API对象。

查看Woker节点

```
kubectl get nodes
```

获取特定节点（node1）的详细信息

```
kubectl describe nodes node1
```

