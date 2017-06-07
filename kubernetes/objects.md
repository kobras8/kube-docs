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
* pods 是不可靠的，随时都会delete，服务需要

#### Volume
#### Namespace

### Controllers
Higher-level abstractions, build upon the basic objects, and provide additional functionality and convenience features.
#### ReplicaSet
#### Deployment
#### StatefulSet
#### DaemonSet
#### Job
