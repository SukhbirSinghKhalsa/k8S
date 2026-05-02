## Kubernetes Architecture
<img width="1071" height="912" alt="K8S getting started" src="https://github.com/user-attachments/assets/967d12eb-d593-48fd-b1a1-1720ea464c05" />


## Docker Image
- consist of os, dependencies, application
- platform independent

## KUBERNETES
- ORCHESTRATION	
- Written in Golang
- Automate application deployment, scaling, management

## Pod
- smallest unit of Kubernetes
- pod is wrapper around container
- single pod can have multiple containers which shares common storage, network, resources

## Architecture of Kubernetes
### Master Node(Control Plane)
1 Kuber Api server
2 Kuber Scheduler
3 Controller Manager
4 ETCD Database

#### Api server
- entry point
- authenticate request
- validate request
- perform all actions within the cluster

#### Scheduler
- decides right node for the pod

#### Controller Manager
- Brain of Kubernetes
- it has variety of controllers like node , pv, replication, deployment, replica set, namespace, service account, job controller, etc

#### node controller
- monitor status of node
- take necessary action of recreate desired number of nodes
- node controller - desired number of nodes maintainence

#### Replication Controller
- monitor status of pod
- take necessary action to recreate desired no pods

#### ETCD Database
- have all the information
- like cluster info, pods, nodes, ips, application, deployment
- no sql db
- stores data in key value pair
- ETCDCTL client - cmd line to access data inside etcd
- only kube api server can directly interact with ETCD database


### Worker Node
1 kubelet
2 kube Proxy
3 container runtime (docker)

#### kubelet
- All activity of nodes
- manager of node
- kube api server request to kubelet for pod creation, after creation it inform kube api-server and it then updated ETCD db with that information

####  kube Proxy
- Responsible for communication between pods


####  container runtime (docker)


```bash
Kube-api server --> pod --> kube-scheduler -->api server --> kubelet --> docker runtime --> api server --> etcd database
```
