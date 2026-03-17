# Task 1: Create Your First Pod (Nginx)

## Create a file called nginx-pod.yaml:

kind: Pod
apiVersion: v1

metadata:
    name: nginx-pod
    labels:
        app: nginx

spec:
    containers:
    - name: nginx
      image: nginx:latest
      ports:
      - containerPort: 80

## kubectl apply -f nginx-pod.yaml
harry@NEW4090-G8:~/my-docker-project/kubernetes-practice/nginx$ kubectl apply -f nginx-pod.yml 
pod/nginx-pod created

## kubectl get pods
harry@NEW4090-G8:~/my-docker-project/kubernetes-practice/nginx$ kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          35s

## kubectl get pods -o wide
harry@NEW4090-G8:~/my-docker-project/kubernetes-practice/nginx$ kubectl get pods -o wide
NAME        READY   STATUS    RESTARTS   AGE   IP           NODE                 NOMINATED NODE   READINESS GATES
nginx-pod   1/1     Running   0          45s   10.244.2.2   tws-cluster-worker   <none>           <none>

# Detailed info about the pod
kubectl describe pod nginx-pod
<img width="652" height="301" alt="image" src="https://github.com/user-attachments/assets/2b6aeab9-2228-4b31-ac20-678564e992a1" />

# Read the logs
kubectl logs nginx-pod

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice/nginx$ kubectl logs nginx-pod
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/03/17 06:34:12 [notice] 1#1: using the "epoll" event method
2026/03/17 06:34:12 [notice] 1#1: nginx/1.29.6
2026/03/17 06:34:12 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19) 
2026/03/17 06:34:12 [notice] 1#1: OS: Linux 6.6.87.2-microsoft-standard-WSL2
2026/03/17 06:34:12 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/03/17 06:34:12 [notice] 1#1: start worker processes
2026/03/17 06:34:12 [notice] 1#1: start worker process 33
2026/03/17 06:34:12 [notice] 1#1: start worker process 34
2026/03/17 06:34:12 [notice] 1#1: start worker process 35
2026/03/17 06:34:12 [notice] 1#1: start worker process 36
2026/03/17 06:34:12 [notice] 1#1: start worker process 37
2026/03/17 06:34:12 [notice] 1#1: start worker process 38
2026/03/17 06:34:12 [notice] 1#1: start worker process 39
2026/03/17 06:34:12 [notice] 1#1: start worker process 40

# Get a shell inside the container
kubectl exec -it nginx-pod -- /bin/bash
# Inside the container, run:
curl localhost:80
exit

<img width="595" height="307" alt="image" src="https://github.com/user-attachments/assets/cd48cd85-0d8f-4c23-889e-0b9f5ed8b578" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Create a Custom Pod (BusyBox)

## kubectl apply -f busybox-pod.yaml
## kubectl get pods
## kubectl logs busybox-pod

<img width="571" height="109" alt="image" src="https://github.com/user-attachments/assets/481e0a8d-cc16-4f61-82b4-8191a477ec0c" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Imperative vs Declarative

## Create a pod without a YAML file
kubectl run redis-pod --image=redis:latest

## Check it
kubectl get pods

<img width="571" height="98" alt="image" src="https://github.com/user-attachments/assets/a3995967-1343-4566-980a-767c89828787" />


## kubectl get pod redis-pod -o yaml

<img width="341" height="416" alt="image" src="https://github.com/user-attachments/assets/bc92976e-0840-4b55-b9d3-fab2a821688c" />

## kubectl run test-pod --image=nginx --dry-run=client -o yaml

<img width="658" height="199" alt="image" src="https://github.com/user-attachments/assets/a6f3a619-0747-4033-98f9-d2845b96bb31" />

A few fields like status, restartPolicy and dbsPolicy are extra when the pod yml is created via imperative command.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Validate Before Applying

## Check if the YAML is valid without actually creating the resource
kubectl apply -f nginx-pod.yaml --dry-run=client

## Validate against the cluster's API (server-side validation)
kubectl apply -f nginx-pod.yaml --dry-run=server

<img width="649" height="63" alt="image" src="https://github.com/user-attachments/assets/cb33d8fc-29ee-40f0-a45b-1856bfb13936" />

## Now intentionally break your YAML (remove the image field or add an invalid field) and run dry-run again. See what error you get.

<img width="641" height="32" alt="image" src="https://github.com/user-attachments/assets/266969f6-44ec-4bc1-a7df-c7c32141b30b" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: Pod Labels and Filtering

## List all pods with their labels
kubectl get pods --show-labels

<img width="551" height="71" alt="image" src="https://github.com/user-attachments/assets/4426de96-0695-4872-9a61-891ab82db88e" />


## Filter pods by label
kubectl get pods -l app=nginx
kubectl get pods -l environment=dev

<img width="596" height="86" alt="image" src="https://github.com/user-attachments/assets/f9ffdd87-196b-47ec-b043-cf18b2d41b53" />


## Add a label to an existing pod
kubectl label pod nginx-pod environment=production

<img width="655" height="33" alt="image" src="https://github.com/user-attachments/assets/c273fb2f-37ac-4497-9e30-726f980139b9" />


## Verify
kubectl get pods --show-labels

<img width="563" height="77" alt="image" src="https://github.com/user-attachments/assets/d909bb99-a299-4540-860e-5308492fb703" />


## Remove a label
kubectl label pod nginx-pod environment-

<img width="595" height="32" alt="image" src="https://github.com/user-attachments/assets/3f7fe76e-4854-4485-a55b-77a189a9a94f" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 6: Clean Up

## Delete by name
kubectl delete pod nginx-pod
kubectl delete pod busybox-pod
kubectl delete pod redis-pod

<img width="558" height="89" alt="image" src="https://github.com/user-attachments/assets/0f470248-fee7-4790-b01e-8ef94cbcaecf" />

# Verify everything is gone
kubectl get pods

<img width="476" height="36" alt="image" src="https://github.com/user-attachments/assets/bf8bf0fa-a018-49b5-878c-94c6fbff41d4" />
