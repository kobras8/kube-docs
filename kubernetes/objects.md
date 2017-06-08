### Basic objects

#### Pod
最小的部署单元。
* 由一个或者多个 container，Unique IP，存储资源等构成。支持包括 Docker 在内的多种容器方案。
* *A Pod represents a running process on your cluster*。
* 需要说明的是，当一个 pod 运行多个 container 时（高级用法），container 共享 network 和 storage 等资源。 举个例子，一个 container 做文件服务器，另外一个 container 更新文件，有点类似多进程互相协作的模式。
* *The Pod wraps these containers and storage resources together as a single manageable entity. Containers inside a Pod can communicate with one another using localhost.All containers in the Pod can access the shared volumes, allowing those containers to share data*
* Pod 本身不支持 self-healing，靠的是更高层的 controller 做的。
* [Init Containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

#### Service
根据`Label Selector`将一组 pods统一对外提供服务
* pods 是不可靠的，随时都会delete，服务需要统一的，持久的服务出口，比如{IP:PORT}
```kind: Service
apiVersion: v1
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```
* 有时，service 也不需要`Label Selector`, 特别是当 service 是一些 kubernetes 集群外的依赖，比如阿里云的 rds. *you can define a service without a selector:*
* *Services are a “layer 4” (TCP/UDP over IP) construct;  the Ingress API was added (beta) to represent “layer 7” (HTTP) services*
*  service discovery: 1. 采用环境变量，2. **DNS，每个 service 分配一个 domain name，集群中的任何一个 pod 都可以通过 dns lookup 访问到这个 service**
*  Headless service: service 没有指定 cluster IP，kube-proxy 不会起任何作用，同时也不会有 load balance。DNS 根据 service 定义的 selector 来自动进行配置。
*  Service types
	* ClusterIP：Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster. This is the default ServiceType
	* NodePort: Exposes the service on each Node’s IP at a static port (the NodePort). A ClusterIP service, to which the NodePort service will route, is automatically created. You’ll be able to contact the NodePort service, from outside the cluster, by requesting `<NodeIP>:<NodePort>`. 在宿主机开一个端口，将内部的服务暴露出来。
	* LoadBalancer: Exposes the service externally using a cloud provider’s load balancer. NodePort and ClusterIP services, to which the external load balancer will route, are automatically created. 可以使用阿里云的 SLB 做为 LoadBalancer。
	* ExternalName: Maps the service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up. This requires version 1.7 or higher of kube-dns.
* ClusterIP 是基础，一般来说，所有service types都会有一个 ClusterIP，如果想要集群外部可以访问到 service，可以使用 NodePort，会把服务在每个节点上都开一个端口。再进一步，可以通过云服务商提供的 Load balancer （比如阿里云的 SLB）将多个 NodePort service 作为一个整体对外提供。
#### Volume
* container 存储的内容都是临时的，需要持久化存储
* 一个 pod 的多个 containers 可以访问 volume
* Volume type，除了云存储外，还支持emptyDir，hostPath，gitRepo，secret 等

#### Namespace
* Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces.


### Controllers
Higher-level abstractions, build upon the basic objects, and provide additional functionality and convenience features.
#### ReplicaSet
* 下一代的 replica controller，支持 set_based 的 label selector
* 保证 replica 的数量
* 使用`Deployment`来做 pod 的编排工作，`ReplicaSet`包含其中，它不会单独被使用
* [horizontal-pod-autoscale](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
#### Deployment
#### StatefulSet
#### DaemonSet
#### Job

### Misc
#### Label Selector
* 对所有的 objects (比如 pod)提供一种松散的管理方式
* TODO: Best Practce
#### Annotations