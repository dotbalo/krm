# 更简洁、更好用、更完善
KRM是一个Kubernetes多集群资源管理平台，基于管理Kubernetes的资源开发，
可以管理Kubernetes的Namespace、Deployment、DaemonSet、StatefulSet、Service、Ingress、Pods、Nodes、CronJob等。

KRM主要实现的是使用图形化界面管理所有的Kubernetes的资源，降低Kubernetes的复杂度。
同时具备了一些常用的功能，比如跨集群资源复制、一键项目迁移、图形化资源编辑、资源一键回滚及更新、多集群资源统计等。
### 项目演示地址
[http://demo.kubeasy.com](http://demo.kubeasy.com/)

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
````
也可以采用手动部署的方式，用来做更加详细的配置
[手动部署文档](https://github.com/dotbalo/krm/blob/main/deploy.md)

### 测试账号请从下面联系方式获取，进群后联系宽哥（如果想要开发一个类似的平台，也可以进群了解）
![image](https://github.com/dotbalo/krm/assets/25141522/d92d9eda-478b-49b6-9e5b-c4a5ef7d7f7a)

### 平台相关截图
#### 登录页
![](https://img2023.cnblogs.com/blog/1095387/202305/1095387-20230528114113524-1891694505.png)

#### 首页
![](https://img2023.cnblogs.com/blog/1095387/202305/1095387-20230528114123121-649789755.png)

#### 跨集群资源复制
![](https://img2023.cnblogs.com/blog/1095387/202305/1095387-20230528114132874-1479426454.png)

#### 资源创建
![](https://img2023.cnblogs.com/blog/1095387/202305/1095387-20230528114142132-1837575048.png)

#### 拓扑图
![](https://img2023.cnblogs.com/blog/1095387/202305/1095387-20230528114149836-1765940398.png)
