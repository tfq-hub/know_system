## minikube

文档：https://minikube.sigs.k8s.io/docs/start/

按照文档安装启动

简化一下 kubectl 命令

```
sudo ln -s $(which minikube) /usr/local/bin/kubectl
```

### 图形管理界面

```
minikube dashboard
```

### 部署一个应用

```
kubectl create deployment hello-world --image=nginx  # 创建一个nginx
kubectl expose deployment hello-world --type=NodePort --port=80  # 暴露端口
kubectl get services hello-world  # 查看应用
minikube service hello-world  # 启动应用
```

### 删除应用

```
kubectl delete deployment hello-world  # 删除应用
kubectl get svc | grep -i hello-world  # 查看服务
kubectl delete svc hello-world  # 删除部署的服务
```

### 安装kubeflow

官网文档：https://www.kubeflow.org/docs/started/workstation/minikube-linux/

遇到报错：

```
INFO[0000] Downloading https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_k8s_istio.v1.2.0.yaml to /tmp/152412265/tmp.yaml  filename="utils/k8utils.go:178"
Error: Cannot determine the object kind:  (kubeflow.error): Code 400 with message: could not fetch specified config https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_k8s_istio.v1.2.0.yaml: Get "https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_k8s_istio.v1.2.0.yaml": dial tcp 0.0.0.0:443: connect: connection refused
Usage:
  kfctl apply -f ${CONFIG} [flags]

Flags:
      --context string   Optional kubernetes context to use when applying resources. Currently not used by KFDef resources.
  -f, --file string      Static config file to use. Can be either a local path:
                         		export CONFIG=./kfctl_gcp_iap.yaml
                         	or a URL:
                         		export CONFIG=https://raw.githubusercontent.com/kubeflow/manifests/v1.0-branch/kfdef/kfctl_gcp_iap.v1.0.0.yaml
                         		export CONFIG=https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_istio_dex.v1.2.0.yaml
                         		export CONFIG=https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_aws.v1.2.0.yaml
                         		export CONFIG=https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_k8s_istio.v1.2.0.yaml
                         	kfctl apply -V --file=${CONFIG}
  -h, --help             help for apply
  -V, --verbose          verbose output default is false

kfctl exited with error: Cannot determine the object kind:  (kubeflow.error): Code 400 with message: could not fetch specified config https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_k8s_istio.v1.2.0.yaml: Get "https://raw.githubusercontent.com/kubeflow/manifests/v1.2-branch/kfdef/kfctl_k8s_istio.v1.2.0.yaml": dial tcp 0.0.0.0:443: connect: connection refused
```

问题分析：这个文件下载失败，应该是官网没改路径

解决方法：

先下载源码：https://github.com/kubeflow/manifests/releases

yaml文件在目录：manifests-1.2.0/kfdef/kfctl_k8s_istio.v1.2.0.yaml

复制到上面的kf-app目录下面，直接启动命令

```
sudo kfctl apply -f kfctl_k8s_istio.v1.2.0.yaml
```

