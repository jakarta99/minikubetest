# minikubetest

## VirtualBox
安裝 VirtualBox, Download from (https://www.virtualbox.org/wiki/Linux_Downloads)

```
vboxmanange --version
```

因為 BIOS 內部的 CPU 設定可能會需要 enable 模擬相關的虛擬化設定。

## Kubectl

Ref: https://kubernetes.io/docs/tasks/tools/install-kubectl/

下載最新的 stable 版本
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

更改為 execute 模式
```
chmod +x ./kubectl
```

安裝到 /usr/local/bin 目錄之下
```
sudo mv ./kubectl /usr/local/bin/kubectl
```

進行測試
```
kubectl version
```

或是直接使用 apt-get
```
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

## Minikube

Ref: (https://kubernetes.io/docs/tasks/tools/install-minikube/)

下載最新的
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
```

安裝之
```
sudo install minikube /usr/local/bin
```
啟動 minikube
```
minikube start --extra-config=apiserver.authorization-mode=RBAC
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default
```
不加上 authorization mode 可能啟動 dashboard 會有 Temporary Error: unexpected response code: 503 的異常
(https://gist.github.com/F21/08bfc2e3592bed1e931ec40b8d2ab6f5)

測試 minikube 啟動結果
```
minikube status
```

啟動 Dashboard
```
minikube dashboard
```


