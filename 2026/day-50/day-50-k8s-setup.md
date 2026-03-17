# Task 1: Recall the Kubernetes Story
Before touching a terminal, write down from memory:

## Why was Kubernetes created? What problem does it solve that Docker alone cannot?
Kubernetes was created to help scale the environament dynamically and self heal. Docker can't help scale automatically.

## Who created Kubernetes and what was it inspired by?
Kubernetes was created by google and it was made open source in 2014. It was inspire by Borg that google used to scale and maintain their applications.

## What does the name "Kubernetes" mean?
"Kubernetes" meaning is pilot i.e. automatically managing application.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Draw the Kubernetes Architecture

<img width="616" height="368" alt="image" src="https://github.com/user-attachments/assets/3401f450-bbd5-4a48-b7bc-83f786df4b9d" />


## What happens when you run kubectl apply -f pod.yaml? Trace the request through each component.

kubectl apply -f pod.yml creates pod for the image mationed in the yml file. Below is the trace:

1. kubectl request reach the API server to create pod, API server asks Scheduler to create pod. 
2. Scheduler asks API server to check with etcd if any worker is free to create the pod. Then API server checks with etcd database.
3. Then as per etcd repose, scheduler reach kubelet to create a pod.
4. kubelet create the pod and updated back API server.

## What happens if the API server goes down?

If API server goes down, control plane stops controllong the pods. Which ever pod is down will continue untill it crash. Scaling can't be done.

## What happens if a worker node goes down?
API server doesn't get its status and it considers the worker dead. So, it created pods on other healthy nodes to compenste the loss of pods.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Install kubectl
kubectl is the CLI tool you will use to talk to your Kubernetes cluster.

# Verify:
# kubectl version --client

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl version --client
Client Version: v1.35.2
Kustomize Version: v5.7.1


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Set Up Your Local Cluster
Choose one of the following. Both give you a fully functional Kubernetes cluster on your machine.
Option A: kind (Kubernetes in Docker)

# kubectl cluster-info
harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:38595
CoreDNS is running at https://127.0.0.1:38595/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

# kubectl get nodes
harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl get nodes
NAME                        STATUS   ROLES           AGE   VERSION
tws-cluster-control-plane   Ready    control-plane   13h   v1.35.0
tws-cluster-worker          Ready    <none>          13h   v1.35.0
tws-cluster-worker2         Ready    <none>          13h   v1.35.0
tws-cluster-worker3         Ready    <none>          13h   v1.35.0

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: Explore Your Cluster
Now that your cluster is running, explore it:

# See cluster info
# kubectl cluster-info

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:38595
CoreDNS is running at https://127.0.0.1:38595/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

# List all nodes
# kubectl get nodes

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl get nodes
NAME                        STATUS   ROLES           AGE   VERSION
tws-cluster-control-plane   Ready    control-plane   20h   v1.35.0
tws-cluster-worker          Ready    <none>          20h   v1.35.0
tws-cluster-worker2         Ready    <none>          20h   v1.35.0
tws-cluster-worker3         Ready    <none>          20h   v1.35.0


# Get detailed info about your node
# kubectl describe node <node-name>

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl describe node tws-cluster-control-plane
Name:               tws-cluster-control-plane
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=tws-cluster-control-plane
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 15 Mar 2026 23:09:49 +0530
Taints:             node-role.kubernetes.io/control-plane:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  tws-cluster-control-plane
  AcquireTime:     <unset>
  RenewTime:       Mon, 16 Mar 2026 19:45:00 +0530
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Mon, 16 Mar 2026 19:41:19 +0530   Sun, 15 Mar 2026 23:09:47 +0530   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Mon, 16 Mar 2026 19:41:19 +0530   Sun, 15 Mar 2026 23:09:47 +0530   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Mon, 16 Mar 2026 19:41:19 +0530   Sun, 15 Mar 2026 23:09:47 +0530   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Mon, 16 Mar 2026 19:41:19 +0530   Sun, 15 Mar 2026 23:10:26 +0530   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  172.18.0.3
  Hostname:    tws-cluster-control-plane
Capacity:
  cpu:                8
  ephemeral-storage:  1055762868Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             16216284Ki
  pods:               110
Allocatable:
  cpu:                8
  ephemeral-storage:  1055762868Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             16216284Ki
  pods:               110
System Info:
  Machine ID:                 266f3f9243dd4bcceea107ba69968
  System UUID:                266f3f9243dd4bcceea107ba69968
  Boot ID:                    7abd8ad2-f1f3-439b-98a8-014c76dd84cf
  Kernel Version:             6.6.87.2-microsoft-standard-WSL2
  OS Image:                   Debian GNU/Linux 12 (bookworm)
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  containerd://2.2.0
  Kubelet Version:            v1.35.0
  Kube-Proxy Version:         
PodCIDR:                      10.244.0.0/24
PodCIDRs:                     10.244.0.0/24
ProviderID:                   kind://docker/tws-cluster/tws-cluster-control-plane
Non-terminated Pods:          (9 in total)
  Namespace                   Name                                                 CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                   ----                                                 ------------  ----------  ---------------  -------------  ---
  kube-system                 coredns-7d764666f9-2nw2x                             100m (1%)     0 (0%)      70Mi (0%)        170Mi (1%)     20h
  kube-system                 coredns-7d764666f9-dgpgp                             100m (1%)     0 (0%)      70Mi (0%)        170Mi (1%)     20h
  kube-system                 etcd-tws-cluster-control-plane                       100m (1%)     0 (0%)      100Mi (0%)       0 (0%)         20h
  kube-system                 kindnet-m69sn                                        100m (1%)     100m (1%)   50Mi (0%)        50Mi (0%)      20h
  kube-system                 kube-apiserver-tws-cluster-control-plane             250m (3%)     0 (0%)      0 (0%)           0 (0%)         20h
  kube-system                 kube-controller-manager-tws-cluster-control-plane    200m (2%)     0 (0%)      0 (0%)           0 (0%)         20h
  kube-system                 kube-proxy-vt5hl                                     0 (0%)        0 (0%)      0 (0%)           0 (0%)         20h
  kube-system                 kube-scheduler-tws-cluster-control-plane             100m (1%)     0 (0%)      0 (0%)           0 (0%)         20h
  local-path-storage          local-path-provisioner-67b8995b4b-k6wjn              0 (0%)        0 (0%)      0 (0%)           0 (0%)         20h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                950m (11%)  100m (1%)
  memory             290Mi (1%)  390Mi (2%)
  ephemeral-storage  0 (0%)      0 (0%)
  hugepages-1Gi      0 (0%)      0 (0%)
  hugepages-2Mi      0 (0%)      0 (0%)
Events:              <none>


# List all namespaces
# kubectl get namespaces

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl get namespaces
NAME                 STATUS   AGE
default              Active   20h
flask-app            Active   17h
kube-node-lease      Active   20h
kube-public          Active   20h
kube-system          Active   20h
local-path-storage   Active   20h


# See ALL pods running in the cluster (across all namespaces)
# kubectl get pods -A

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl get pods -A
NAMESPACE            NAME                                                READY   STATUS    RESTARTS       AGE
default              nginx-pod                                           1/1     Running   1 (8h ago)     19h
flask-app            flask-app                                           1/1     Running   1 (8h ago)     17h
flask-app            flask-app-deployment-6d44747767-7jk7x               1/1     Running   1 (8h ago)     17h
flask-app            flask-app-deployment-6d44747767-tshms               1/1     Running   1 (8h ago)     17h
kube-system          coredns-7d764666f9-2nw2x                            1/1     Running   1 (8h ago)     20h
kube-system          coredns-7d764666f9-dgpgp                            1/1     Running   1 (8h ago)     20h
kube-system          etcd-tws-cluster-control-plane                      1/1     Running   1 (8h ago)     20h
kube-system          kindnet-4n6t8                                       1/1     Running   1 (8h ago)     20h
kube-system          kindnet-7msh4                                       1/1     Running   1 (8h ago)     20h
kube-system          kindnet-g4wvc                                       1/1     Running   1 (8h ago)     20h
kube-system          kindnet-m69sn                                       1/1     Running   1 (8h ago)     20h
kube-system          kube-apiserver-tws-cluster-control-plane            1/1     Running   1 (8h ago)     20h
kube-system          kube-controller-manager-tws-cluster-control-plane   1/1     Running   2 (121m ago)   20h
kube-system          kube-proxy-dwpkt                                    1/1     Running   1 (8h ago)     20h
kube-system          kube-proxy-llxzm                                    1/1     Running   1 (8h ago)     20h
kube-system          kube-proxy-nmc8j                                    1/1     Running   1 (8h ago)     20h
kube-system          kube-proxy-vt5hl                                    1/1     Running   1 (8h ago)     20h
kube-system          kube-scheduler-tws-cluster-control-plane            1/1     Running   2 (121m ago)   20h
local-path-storage   local-path-provisioner-67b8995b4b-k6wjn             1/1     Running   2 (8h ago)     20h

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Look at the pods running in the kube-system namespace:

kubectl get pods -n kube-system
You should see pods like etcd, kube-apiserver, kube-scheduler, kube-controller-manager, coredns, and kube-proxy. These are the architecture components you drew in Task 2 — running as pods inside the cluster.

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl get pods -n kube-system
NAME                                                READY   STATUS    RESTARTS       AGE
coredns-7d764666f9-2nw2x                            1/1     Running   1 (8h ago)     20h
coredns-7d764666f9-dgpgp                            1/1     Running   1 (8h ago)     20h
etcd-tws-cluster-control-plane                      1/1     Running   1 (8h ago)     20h
kindnet-4n6t8                                       1/1     Running   1 (8h ago)     20h
kindnet-7msh4                                       1/1     Running   1 (8h ago)     20h
kindnet-g4wvc                                       1/1     Running   1 (8h ago)     20h
kindnet-m69sn                                       1/1     Running   1 (8h ago)     20h
kube-apiserver-tws-cluster-control-plane            1/1     Running   1 (8h ago)     20h
kube-controller-manager-tws-cluster-control-plane   1/1     Running   2 (126m ago)   20h
kube-proxy-dwpkt                                    1/1     Running   1 (8h ago)     20h
kube-proxy-llxzm                                    1/1     Running   1 (8h ago)     20h
kube-proxy-nmc8j                                    1/1     Running   1 (8h ago)     20h
kube-proxy-vt5hl                                    1/1     Running   1 (8h ago)     20h
kube-scheduler-tws-cluster-control-plane            1/1     Running   2 (126m ago)   20h

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
