<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [单机部署](#%E5%8D%95%E6%9C%BA%E9%83%A8%E7%BD%B2)
  - [安装 kubectl](#%E5%AE%89%E8%A3%85-kubectl)
  - [使用 Minikube 部署 Kubernetes](#%E4%BD%BF%E7%94%A8-minikube-%E9%83%A8%E7%BD%B2-kubernetes)
    - [安装](#%E5%AE%89%E8%A3%85)
    - [验证](#%E9%AA%8C%E8%AF%81)
  - [使用 Kind 部署 Kubernetes](#%E4%BD%BF%E7%94%A8-kind-%E9%83%A8%E7%BD%B2-kubernetes)
    - [安装](#%E5%AE%89%E8%A3%85-1)
    - [验证](#%E9%AA%8C%E8%AF%81-1)
  - [其它开源安装工具](#%E5%85%B6%E5%AE%83%E5%BC%80%E6%BA%90%E5%AE%89%E8%A3%85%E5%B7%A5%E5%85%B7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 单机部署

## 安装 kubectl

Kubectl 是 Kubernetes 自带的命令行工具，可以用它直接操作 Kubernetes。当前最新版本支持 Kubernetes v1.33。

macOS，执行：

```bash
# 使用 Homebrew（推荐）https://brew.sh/
brew install kubectl
# 或者使用完整包名
brew install kubernetes-cli
```

验证安装：

```bash
kubectl version --client
```

Linux，执行：

```bash
# 获取最新稳定版本
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/
```

Windows，执行：

```bash
# 获取最新稳定版本
curl.exe -LO "https://dl.k8s.io/release/$(curl.exe -L -s https://dl.k8s.io/release/stable.txt)/bin/windows/amd64/kubectl.exe"
```

## 使用 Minikube 部署 Kubernetes

[Minikube](https://github.com/kubernetes/minikube) 用于本地部署 kubernetes 集群，支持 macOS，Linux，和 Windows。

**系统要求**：
- 建议预留至少 60-80 GB 可用磁盘空间（官方最低要求 20 GB）
- Docker Desktop（个人使用免费）或其他容器运行时

### 安装

**macOS**：

```bash
# 使用 Homebrew（推荐）
brew install minikube

# Intel Mac 手动安装
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube

# Apple Silicon (M1/M2) Mac 手动安装
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-darwin-arm64
sudo install minikube-darwin-arm64 /usr/local/bin/minikube
```

**Linux**：

```bash
# 使用 curl
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

**Windows**：

```bash
# 使用 chocolatey
choco install minikube

# 或下载安装程序
# 访问 https://github.com/kubernetes/minikube/releases/latest 下载 minikube-installer.exe
```

**确认 minikube 版本**：

```sh
$ minikube version
minikube version: v1.34.0
commit: cfd61e485f923ba79b3ba3d9ed4f7bed5df8da9d
```

**启动 Minikube**：

```sh
$ minikube start
😄  minikube v1.34.0 on darwin (amd64)
✨  Using the docker driver based on existing profile
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image ...
🔄  Restarting existing docker container for "minikube" ...
🐳  Preparing Kubernetes v1.33.3 on Docker 25.0.3 ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

### 验证

执行下面的命令：

```sh
$ kubectl get nodes
NAME       STATUS   ROLES           AGE    VERSION
minikube   Ready    control-plane   4m5s   v1.33.3
```

若输出正常，则表示创建成功。注意 v1.33.3 是当前最新版本，角色显示为 `control-plane`（替代了旧的 `master` 术语）。

## 使用 Kind 部署 Kubernetes

[Kind](https://github.com/kubernetes-sigs/kind) (Kubernetes in Docker) 是另一个 Kubernetes 集群部署工具，通过 Docker 容器 "nodes" 完成部署。主要用于测试 Kubernetes 本身，也适用于本地开发或 CI。

**系统要求**：
- Docker、Podman 或 nerdctl
- 可选：Go 1.17+ （如果要从源码安装）

### 安装

**macOS**：

```bash
# 使用 Homebrew（推荐）
brew install kind

# Intel Mac 手动安装
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-darwin-amd64

# Apple Silicon (M1/M2) Mac 手动安装
[ $(uname -m) = arm64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-darwin-arm64

# 设置可执行权限并移动到 PATH
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

**如果已安装 Go 1.17+**：

```bash
go install sigs.k8s.io/kind@v0.29.0
```

**创建集群**：

```sh
$ kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.33.0) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind
```

**注意**: Kind 会自动配置 kubectl 上下文，无需手动设置 KUBECONFIG。

### 验证

执行下面的命令：

```sh
$ kubectl get nodes
NAME                 STATUS   ROLES           AGE     VERSION
kind-control-plane   Ready    control-plane   2m54s   v1.33.0
```

若输出正常，则表示创建成功。注意角色显示为 `control-plane`（替代了旧的 `master` 术语）。

## 其它开源安装工具

- https://github.com/bsycorp/kind
- https://github.com/ubuntu/microk8s
- https://github.com/kinvolk/kube-spawn
- https://github.com/danderson/virtuakube
- https://github.com/kubernetes-sigs/kubeadm-dind-cluster
