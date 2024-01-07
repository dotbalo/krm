# KRM部署
KRM采用前后端分离架构，前端使用Vue实现，后端使用Go实现。

KRM安装时需要把服务安装到Kubernetes集群当中，之后可以在KRM中添加被管理的集群，所以要求KRM所在的集群需要和其它被管理的集群的APIServer能够通信，其它无要求，安装无侵入。

## 服务部署
在安装KRM的集群中创建Namespace，并授权
````
kubectl create ns krm
kubectl create sa krm-backend -n krm
kubectl create rolebinding krm-backend --clusterrole=edit --serviceaccount=krm:krm-backend --namespace=krm
````
部署后端服务
````
cat<<EOF | kubectl -n krm apply -f -
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: krm-backend
  name: krm-backend
spec:
  ports:
  - name: http
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: krm-backend
  sessionAffinity: None
  type: ClusterIP
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: krm-backend
  name: krm-backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: krm-backend
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: krm-backend
    spec:
      serviceAccountName: krm-backend
      containers:
      - env:
        - name: TZ
          value: Asia/Shanghai
        - name: LANG
          value: C.UTF-8
        - name: GIN_MODE
          value: release
        - name: LOG_LEVEL
          value: info
        - name: USERNAME
          value: 21232F297A57A5A743894A0E4A801FC3
        - name: PASSWORD
          value: 21232F297A57A5A743894A0E4A801FC3
        - name: "IN_CLUSTER"
          value: "true"
        image: registry.cn-beijing.aliyuncs.com/dotbalo/krm-backend:v0.0.4
        lifecycle: {}
        livenessProbe:
          failureThreshold: 2
          initialDelaySeconds: 10
          periodSeconds: 10
          successThreshold: 1
          tcpSocket:
            port: 8080
          timeoutSeconds: 2
        name: krm-backend
        ports:
        - containerPort: 8080
          name: web
          protocol: TCP
        readinessProbe:
          failureThreshold: 2
          initialDelaySeconds: 10
          periodSeconds: 10
          successThreshold: 1
          tcpSocket:
            port: 8080
          timeoutSeconds: 2
        resources:
          limits:
            cpu: 1
            memory: 1024Mi
          requests:
            cpu: 200m
            memory: 256Mi
      restartPolicy: Always
EOF
````
部署前端服务
````
cat<<EOF | kubectl -n krm apply -f -
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: krm-frontend
  name: krm-frontend
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: krm-frontend
  sessionAffinity: None
  type: NodePort
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: krm-frontend
  name: krm-frontend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: krm-frontend
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: krm-frontend
    spec:
      containers:
      - env:
        - name: TZ
          value: Asia/Shanghai
        - name: LANG
          value: C.UTF-8
        image: registry.cn-beijing.aliyuncs.com/dotbalo/krm-frontend:v0.0.4
        lifecycle: {}
        livenessProbe:
          failureThreshold: 2
          initialDelaySeconds: 10
          periodSeconds: 10
          successThreshold: 1
          tcpSocket:
            port: 80
          timeoutSeconds: 2
        name: krm-backend
        ports:
        - containerPort: 80
          name: web
          protocol: TCP
        readinessProbe:
          failureThreshold: 2
          initialDelaySeconds: 10
          periodSeconds: 10
          successThreshold: 1
          tcpSocket:
            port: 80
          timeoutSeconds: 2
        resources:
          limits:
            cpu: 1
            memory: 512Mi
          requests:
            cpu: 100m
            memory: 256Mi
      restartPolicy: Always
EOF
````
部署成功后，通过kubectl get svc -n krm查看krm-frontend的Service的NodePort，之后通过任意一台Kubernetes工作节点的IP:NodePort即可访问KRM

默认用户名密码：admin / admin

## 配置域名
如果集群中有Ingress或者其它网关服务，可以自行配置访问域名，比如使用ingress-nginx
````
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: krm
  namespace: krm
spec:
  rules:
    - host: demo.kubeasy.com
      http:
        paths:
          - backend:
              service:
                name: krm-frontend
                port:
                  number: 80
            path: /
            pathType: Prefix
  ingressClassName: nginx
````

## 添加管理集群
点击集群管理--添加，之后添加集群信息即可

![image](https://github.com/dotbalo/krm/assets/25141522/00e48c89-6847-4b76-97f4-dc1b4b049ea9)
