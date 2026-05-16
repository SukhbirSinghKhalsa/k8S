## Kubernetes Architecture

smallest unit with computing methods:

- virtualization   -- virtual machine
- Containerization -- container
- Orchestration    --  pod

- cli tool used in k8s is kubectl
- k8s is created with the help of GO language

- 4 master component, 3 worker components

- master components: api-server, scheduler, controller, etcd, Cloud-Controller-Manager

- worker components: kubelet, kube-proxy, container runtime (CRI)
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

## Revision - More detailed
# Kubernetes Architecture

## Control Plane Components

### API Server

Central communication hub of Kubernetes.

All components communicate through the API Server.

#### Handles

* Authentication
* Authorization
* Admission Control

---

## Admission Controllers

Used to validate or modify requests before objects are stored.

### Mutating Admission Controller

Modifies requests.

#### Examples

* Adds labels
* Injects sidecars
* Updates YAML configurations automatically

### Validating Admission Controller

Validates requests.

#### Responsibilities

* Ensures configuration is correct before deployment
* Rejects invalid configurations

---

## ETCD

Distributed key-value database.

* Stores all cluster data
* Source of truth for the Kubernetes cluster

---

## Scheduler

Responsible for pod scheduling.

* Finds healthy worker nodes for pods
* Default decision maker for pod placement

### Scheduler Considers

* Node Affinity
* Node Selector
* Pod Affinity / Anti-Affinity
* Resource availability

> **Important:**
> Scheduler can be bypassed manually using specific mechanisms.

---

## Controller Manager

Maintains desired cluster state.

### Ensures

* Desired replica count
* Pods stay running
* Failed pods are recreated

### Workflow

* Kubelet sends node/pod status to API Server
* Controller Manager continuously checks cluster state
* Takes corrective action if actual state differs from desired state

---

# Worker Node Components

## Kubelet

Agent running on each worker node.

### Responsibilities

* Ensures containers remain healthy and running
* Communicates with API Server
* Orders CRI to pull container images

---

## CRI (Container Runtime Interface)

Responsible for:

* Pulling images
* Creating containers
* Managing container runtime

### Example Runtime

* `containerd`

---

## CNI (Container Network Interface)

Handles pod networking.

### Responsibilities

* Assigns private IP addresses to pods
* Enables internal pod-to-pod communication

---

## CSI (Container Storage Interface)

Connects Kubernetes with external storage systems.

### Responsibilities

* Handles persistent storage communication

---

## Kube Proxy

Manages networking rules and iptables.

### Responsibilities

* Routes external traffic to pods
* Load balances traffic between pods
* Maintains networking rules

### Example

`External Request → Service → Correct Pod`

---

# Simple Draw.io Layout Suggestion

```text
                    +----------------------+
                    |      API Server      |
                    | Auth/Authz/Admission |
                    +----------+-----------+
                               |
        +----------------------+----------------------+
        |                      |                      |
+-------v-------+     +--------v--------+    +--------v--------+
|     ETCD      |     |   Scheduler     |    | Controller Mgr  |
| Key-Value DB  |     | Pod Placement   |    | Desired State   |
+---------------+     +-----------------+    +-----------------+


                    WORKER NODE
    +--------------------------------------------------+
    |                  Kubelet                         |
    |--------------------------------------------------|
    | CRI  -> Pull Images / Create Containers          |
    | CNI  -> Networking / Private IP                  |
    | CSI  -> External Storage                         |
    | Kube Proxy -> Traffic Routing / IPTables         |
    +--------------------------------------------------+
```
