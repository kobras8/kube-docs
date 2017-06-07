### Feature
#### Automatic binpacking
根据容器使用的资源和一些约束条件，自动将容器装配部署
*Automatically places containers based on their resource requirements and other constraints, while not sacrificing availability. Mix critical and best-effort workloads in order to drive up utilization and save even more resources*
#### Self-healing
根据容器或者宿主机的状态来保证服务健康
*Restarts containers that fail, replaces and reschedules containers when nodes die, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.*
#### Horizontal scaling
自动扩容
*Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.*
#### Service discovery and load balancing
对于特定服务，通过内部 DNS 的方式做负载均衡和服务发现
*No need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives containers their own IP addresses and a single DNS name for a set of containers, and can load-balance across them.*
#### Automated rollouts and rollbacks
灰度上线，遇到问题，自动回滚
*Kubernetes progressively rolls out changes to your application or its configuration, while monitoring application health to ensure it doesn't kill all your instances at the same time. If something goes wrong, Kubernetes will rollback the change for you. Take advantage of a growing ecosystem of deployment solutions.*
#### Secret and configuration management
密码和配置管理
*Deploy and update secrets and application configuration without rebuilding your image and without exposing secrets in your stack configuration.*
#### Storage orchestration
存储编排，自动挂载本地或者网络存储
*Automatically mount the storage system of your choice, whether from local storage, a public cloud provider such as GCP or AWS, or a network storage system such as NFS, iSCSI, Gluster, Ceph, Cinder, or Flocker.*
#### Batch execution
批处理，job 执行
*In addition to services, Kubernetes can manage your batch and CI workloads, replacing containers that fail, if desired.*