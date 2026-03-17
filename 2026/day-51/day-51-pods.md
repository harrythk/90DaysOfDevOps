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






