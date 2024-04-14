# 更简洁、更好用、更完善
KRM是一个Kubernetes多集群资源管理平台，基于管理Kubernetes的资源开发，
可以管理Kubernetes的Namespace、Deployment、DaemonSet、StatefulSet、Service、Ingress、Pods、Nodes、CronJob、Velero等。

KRM主要实现的是使用图形化界面管理所有的Kubernetes的资源，降低Kubernetes的复杂度。
同时具备了一些常用的功能，比如跨集群资源复制、一键项目迁移、图形化资源编辑、资源一键回滚及更新、多集群资源统计、可视化集群备份和还原等。
### 项目演示地址
[http://demo.kubeasy.com](http://demo.kubeasy.com/)
用户名密码：dukuan / Q_Q727585266

### 免费视频教程
[https://www.bilibili.com/video/BV1Hx421C7nA/](https://www.bilibili.com/video/BV1Hx421C7nA/)


[https://edu.51cto.com/course/35856.html](https://edu.51cto.com/course/35856.html)

### 快速部署
如果想要使用KRM管理自己的集群，可以参考如下步骤进行安装：
````
# 需要自行安装git工具，比如 yum install git或者apt-get install git
git clone https://gitee.com/dukuan/k8s-ha-install.git
cd k8s-ha-install
kubectl  create -f krm.yaml
# 创建成功后，通过kubectl get svc -n krm查看frontend服务的NodePort，之后通过http://任意节点IP:NodePort即可访问
默认用户名密码：admin/admin
````
也可以采用手动部署的方式，用来做更加详细的配置
[手动部署文档](https://github.com/dotbalo/krm/blob/main/deploy.md)
### 版本更新
````
如果部署的KRM版本是latest，直接重新部署即可完成升级（也可以直接删除KRM的前后端Pod即可完成更新）。
如果不是latest版本， 直接把KRM的Deployment的镜像版本均改成latest即可。
````

### 如果想要开发一个类似的平台和有其他问题，可以进群了解
![image](https://github.com/dotbalo/krm/assets/25141522/d92d9eda-478b-49b6-9e5b-c4a5ef7d7f7a)

### 平台相关截图
#### 登录页
![登录页](https://github.com/dotbalo/krm/assets/25141522/adaf1ec2-6046-45d8-81ee-e49476d4e91b)

#### 首页
![首页](https://github.com/dotbalo/krm/assets/25141522/cc773147-06a6-4c03-b5d6-3fb77534d121)


#### 跨集群资源复制
![image](https://github.com/dotbalo/krm/assets/25141522/49c00391-e97c-4cb3-82ed-c6baa8a78172)


#### 资源创建
![image](https://github.com/dotbalo/krm/assets/25141522/f74b1350-2adb-4e9f-a52a-82b3e62d1a15)


#### 拓扑图
![image](https://github.com/dotbalo/krm/assets/25141522/7180baf5-2f06-4bda-b1a8-c60986609c29)

#### 备份管理
![image](https://github.com/dotbalo/krm/assets/25141522/86587673-0395-4476-b560-e626226a170b)

#### 节点管理
![image](https://github.com/dotbalo/krm/assets/25141522/68bef620-bf91-4be9-889a-6a34febd9d20)

#### Pod管理 支持下线功能
![image](https://github.com/dotbalo/krm/assets/25141522/0e72b4a0-49b1-40e5-a0de-23570c86dfab)

#### 调度资源管理 一键式操作
![image](https://github.com/dotbalo/krm/assets/25141522/bcf862dc-17b8-4f34-aec4-5e426894363e)
