## Kuboard 介绍

`Kuboard` 是一款免费的 Kubernetes 管理工具，提供了丰富的功能，结合代码仓库、镜像仓库、CI/CD工具等，可以便捷的搭建一个生产可用的 Kubernetes 容器云平台，轻松管理和运行云原生应用。

![Kuboard-HomePage](/img/preview.png)

Kuboard 提供的功能有：

* Kubernetes 基本管理功能
  * 节点管理
  
  * 名称空间管理
  
  * 存储类/存储卷管理
  
  * 控制器（Deployment、StatefulSet、DaemonSet、CronJob、Job、ReplicaSet）管理
  
  * Service、Ingress 管理
  
  * ConfigMap、Secret 管理
  
  * CustomerResourceDefinition 管理
  
    ![KubernetesManagement](/img/8bc46409f5b244e289b7bc31305e1514.jpeg)
* Kubernetes 问题诊断
  * Top Nodes、Top Pods
  
  * 事件列表及通知
  
  * 容器日志及终端
  
  * KuboardProxy (kubectl proxy 的在线版本)
  
  * PortForward (kubectl port-forward 的快捷版本)
  
  * 复制文件 （kubectl cp 的在线版本）
  
    ![Kubernetes问题诊断](/img/9088c8536c984b67b84c56c9a9fdb686.jpeg)
* 认证与授权
  * Github、GitLab 单点登录
  
  * KeyCloak 认证
  
  * LDAP 认证
  
  * 完整的 RBAC 权限管理
  
    ![Kuboard-RBAC](/img/0fd57872320d46e7a2dd407e429cb181.jpeg)
* Kuboard 特色功能
  * Kuboard 官方套件
    * Grafana+Prometheus 资源监控
    * Grafana+Loki+Promtail 日志聚合
    
  * Kuboard 自定义名称空间布局
  
  * Kuboard 中英文语言包
  
    ![Logging](/img/f480225fccfe4d65b53a508dd0c11ff4.jpeg)

## 活跃的社群

自2019年8月发布以来，随着 Kuboard 功能的日益完善，Kuboard 已经获得 4800+ 和 23w 多的下载。数百家公司正式将 Kuboard 用于生产环境，社群人数 5000 人，Kuboard 相关问题可以第一时间获得社群的帮助以及 Kuboard 开发团队的解答。

Kuboard 开发团队平均一周发布一次版本更新，以最快的速度解决社群用户反馈的问题，并将用户的意见和建议加入到新的版本中。
* [Kuboard 1.0.x 更新日志](/support/v1.0.x)
* [Kuboard 2.0.x 更新日志](/support/v2.0.x)

![stars](/img/kuboard-stars.png)

## 安装前提

Kuboard 只依赖于 Kubernetes API，您可以在多种情况下使用 Kuboard：
* 使用 kubeadm 安装的 Kubernetes 集群
* 使用二进制方式安装的 Kubernetes 集群
* 阿里云/腾讯云等云供应商托管的 Kubernetes 集群

Kuboard 对 Kubernetes 的版本兼容性，如下表所示：

| Kubernetes 版本 | Kuboard 版本   | 兼容性 | 说明                                                         |
| --------------- | -------------- | ------ | ------------------------------------------------------------ |
| v1.18           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😄</span>      | 已验证                            |
| v1.17           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😄</span>      | 已验证                            |
| v1.16           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😄</span>      | 已验证                            |
| v1.15           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😄</span>      | 已验证                            |
| v1.14           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😄</span>      | 已验证                            |
| v1.13           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😄</span>      | 已验证                       |
| v1.12           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😐</span>      | Kubernetes Api v1.12 不支持 dryRun，<br />Kuboard 不支持 Kubernetes v1.12 |
| v1.11           | v1.0.x， v2.0.x | <span style="font-size: 24px;">😐</span>      | Kuboard 不支持 Kubernetes v1.11                                                         |


## 安装

### 安装 Kuboard

``` sh
kubectl apply -f https://kuboard.cn/install-script/kuboard.yaml
kubectl apply -f https://addons.kuboard.cn/metrics-server/0.3.6/metrics-server.yaml
```

### 卸载 Kuboard

``` sh
kubectl delete -f https://kuboard.cn/install-script/kuboard.yaml
kubectl delete -f https://addons.kuboard.cn/metrics-server/0.3.6/metrics-server.yaml
```

## 获取 Token

您可以获得管理员用户、只读用户的Token

### 管理员用户

**拥有的权限**

* 此Token拥有 ClusterAdmin 的权限，可以执行所有操作

**执行命令**

```bash
$ echo $(kubectl -n kube-system get secret $(kubectl -n kube-system get secret | grep kuboard-user | awk '{print $1}') -o go-template='{{.data.token}}' | base64 -d)  
```

**输出**

取输出信息中 token 字段
```{13}
eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLWc4aHhiIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI5NDhiYjVlNi04Y2RjLTExZTktYjY3ZS1mYTE2M2U1ZjdhMGYiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06YWRtaW4tdXNlciJ9.DZ6dMTr8GExo5IH_vCWdB_MDfQaNognjfZKl0E5VW8vUFMVvALwo0BS-6Qsqpfxrlz87oE9yGVCpBYV0D00811bLhHIg-IR_MiBneadcqdQ_TGm_a0Pz0RbIzqJlRPiyMSxk1eXhmayfPn01upPdVCQj6D3vAY77dpcGplu3p5wE6vsNWAvrQ2d_V1KhR03IB1jJZkYwrI8FHCq_5YuzkPfHsgZ9MBQgH-jqqNXs6r8aoUZIbLsYcMHkin2vzRsMy_tjMCI9yXGiOqI-E5efTb-_KbDVwV5cbdqEIegdtYZ2J3mlrFQlmPGYTwFI8Ba9LleSYbCi4o0k74568KcN_w
```


## 访问 Kuboard

您可以通过NodePort、port-forward 两种方式当中的任意一种访问 Kuboard

### 通过NodePort访问

Kuboard Service 使用了 NodePort 的方式暴露服务，NodePort 为 32567；您可以按如下方式访问 Kuboard。

`
http://任意一个Worker节点的IP地址:32567/
`

输入前一步骤中获得的 token，可进入 **Kubernetes 集群概览**

## 进一步使用

请访问 [Kuboard 官网](https://kuboard.cn)，了解如何：

* 利用 Kuboard 管理 Kubernetes 集群；
* 授权用户访问指定的名称空间；
* 让多个团队协作使用 Kuboard 管理 Kubernetes 集群；
* 将 Kuboard/Kubernetes 与 CI/CD 工具整合；
* 利用 Kuboard 进行 Kubernetes 应用程序的问题诊断；
* 使用 Kuboard 监控套件监控 Kubernetes 集群；
* 使用 Kuboard 日志聚合套件查看应用的日志；