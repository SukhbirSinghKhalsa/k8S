## If one pod has multiple container,  then 
- it has same localhost network, so they can communicate with each other using localhost and port number
- they share same storage, so they can read and write to the same volume
- they share same lifecycle, so if one container in the pod crashes, the whole pod will be restarted
- they share same resource limits, so if one container in the pod uses too much CPU or memory, it can affect the other container in the pod
- it has same labels and selectors, so it can be selected by the same service or deployment

## when different pod
- they have different local host


## networking
- after every pod kill, ip address gets changed, how kubernetes manage them?
- we can use service resources - type Cluster IP Service
- What if pod gets killed, we can use Deployment, replicaset, controller, stateful, stateless
- application gateway with public ip - domain --> cluster ip --> pods

## Docker & Kubernetes Networking
- In Docker Individual Containers have their own network and can communicate with each other with the help of their internal ips
- In kubernetes, we have a additional layer of pod inside which we have contianers, so now those individual containers do not get seperate ip addresses, instead the pod get a unique id and then with that we can connect to whatever number of containers are present inside pod with the help of the pod ip addrress

## Scenarios
- can 2 nginx container run inside a same pod? --> no port no collision will happen, as they will have a same port no
- can we run nginx, firefox container inside a same pod --> yes, different port no, we can hit any of those containers with the allocaated Ip address of pod



## Files/ Storage in K8S
- pod are epheremal, it gets killed easily
- and new pod are created, what happens to files inside it?
- files will get removed, okay, so any way to persist them
- we can use azure storage account or any storage with help of PV (persistant volume)
- we can claim PV and mount it to the pod with pvc clain
- pv.yml
- pvc-claim.yml
- pod.yml - mount key

## Cluster Ip Service
- pod load balancing
