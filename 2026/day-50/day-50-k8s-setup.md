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
Unable to paste the photo here


# What happens when you run kubectl apply -f pod.yaml? Trace the request through each component.

kubectl apply -f pod.yml creates pod for the image mationed in the yml file. Below is the trace:

1. kubectl request reach the API server to create pod, API server asks Scheduler to create pod. 
2. Scheduler asks API server to check with etcd if any worker is free to create the pod. Then API server checks with etcd database.
3. Then as per etcd repose, scheduler reach kubelet to create a pod.
4. kubelet create the pod and updated back API server.

# What happens if the API server goes down?

If API server goes down, control plane stops controllong the pods. Which ever pod is down will continue untill it crash. Scaling can't be done.

# What happens if a worker node goes down?
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

