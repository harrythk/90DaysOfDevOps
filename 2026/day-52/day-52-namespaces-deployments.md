# Task 1: Explore Default Namespaces

## Task 1: Explore Default Namespaces

<img width="537" height="110" alt="image" src="https://github.com/user-attachments/assets/917d997c-2dcd-4f31-b961-f070e99692c7" />

## Check what is running inside kube-system
kubectl get pods -n kube-system

<img width="537" height="216" alt="image" src="https://github.com/user-attachments/assets/4ad9b41e-4b8a-4ff1-8052-96b98aff6517" />

## How many pods are running in kube-system?
14 pods are running inside kube-system.

++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Create and Use Custom Namespaces

## kubectl create namespace dev
## kubectl create namespace staging

<img width="521" height="58" alt="image" src="https://github.com/user-attachments/assets/7f112743-31aa-4ad4-be25-8ddf166fa34c" />


## kubectl get namespaces

<img width="465" height="138" alt="image" src="https://github.com/user-attachments/assets/021e08a6-7b69-4173-8c16-800a8f1fc6f6" />

## kubectl apply -f namespace.yaml
<img width="513" height="34" alt="image" src="https://github.com/user-attachments/assets/504dc167-cbf3-4ae6-98e7-d2d453748267" />

## kubectl run nginx-dev --image=nginx:latest -n dev
## kubectl run nginx-staging --image=nginx:latest -n staging

<img width="656" height="63" alt="image" src="https://github.com/user-attachments/assets/01afbd85-13f8-48f0-b653-828199e21ae9" />

## kubectl get pods -A

<img width="695" height="286" alt="image" src="https://github.com/user-attachments/assets/a7662759-3714-4d7b-898a-a1031dd4dc74" />

++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Create Your First Deployment

## kubectl apply -f nginx-deployment.yaml

<img width="599" height="35" alt="image" src="https://github.com/user-attachments/assets/07041c18-ee83-4e9c-8b18-d6feebeb98a9" />


##  kubectl get deployments -n dev
## kubectl get pods -n dev

<img width="545" height="127" alt="image" src="https://github.com/user-attachments/assets/830574ec-6b4e-4b0d-942c-29f3abd41c7e" />

## What do the READY, UP-TO-DATE, and AVAILABLE columns mean in the deployment output?

READY - Number of Pods ready
UP-TO-DATE - Pods running the latest Deployment spec
AVAILABLE - Pods that have been Ready for a minimum time

++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Self-Healing — Delete a Pod and Watch It Come Back

# List pods
kubectl get pods -n dev

<img width="469" height="86" alt="image" src="https://github.com/user-attachments/assets/effedec2-3477-464e-b2f8-f22def42712f" />

# Delete one of the deployment's pods (use an actual pod name from your output)
kubectl delete pod <pod-name> -n dev

harry@NEW4090-G8:~/my-docker-project/kubernetes-practice$ kubectl delete pod nginx-deployment-5d9c84579f-ng56n -n dev
pod "nginx-deployment-5d9c84579f-ng56n" deleted from dev namespace

# Immediately check again
kubectl get pods -n dev

<img width="508" height="85" alt="image" src="https://github.com/user-attachments/assets/68b0fa74-f3fb-484b-8423-2f0a88c10853" />

# Is the replacement pod's name the same as the one you deleted, or different?
Replaced pod's name is different as a new pod was created.

++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Scale the Deployment

# Scale up to 5
kubectl scale deployment nginx-deployment --replicas=5 -n dev
kubectl get pods -n dev

<img width="687" height="137" alt="image" src="https://github.com/user-attachments/assets/0d557223-666f-43b0-9f37-0b1bd5459660" />

# Scale down to 2
kubectl scale deployment nginx-deployment --replicas=2 -n dev
kubectl get pods -n dev

<img width="692" height="98" alt="image" src="https://github.com/user-attachments/assets/0a6778d8-305b-4071-885b-7ea892f6030e" />

++++++++++++++++++++++++++++++++++++++++++++++++

## Task 6: Rolling Update

# kubectl set image deployment/nginx-deployment nginx=nginx:1.25 -n dev

<img width="730" height="30" alt="image" src="https://github.com/user-attachments/assets/9bc7b2f9-d139-4421-a893-255bd20b28dd" />

# kubectl rollout status deployment/nginx-deployment -n dev

<img width="667" height="110" alt="image" src="https://github.com/user-attachments/assets/61908871-483d-44ea-b0e8-eb84ac8ca6ce" />

# kubectl rollout history deployment/nginx-deployment -n dev

<img width="662" height="74" alt="image" src="https://github.com/user-attachments/assets/afc45bda-cd90-4db2-818d-d8026f800277" />


# kubectl rollout undo deployment/nginx-deployment -n dev
# kubectl rollout status deployment/nginx-deployment -n dev

<img width="668" height="129" alt="image" src="https://github.com/user-attachments/assets/9d1e15a8-aba0-4c0b-872e-ccde5b582922" />

# kubectl describe deployment nginx-deployment -n dev | grep Image

<img width="704" height="38" alt="image" src="https://github.com/user-attachments/assets/b9414573-b86b-42b8-b7e8-94f3d3e9a218" />

++++++++++++++++++++++++++++++++++++++++++++++++

## Task 7: Clean Up

kubectl delete deployment nginx-deployment -n dev
kubectl delete pod nginx-dev -n dev
kubectl delete pod nginx-staging -n staging
kubectl delete namespace dev staging production

<img width="616" height="137" alt="image" src="https://github.com/user-attachments/assets/10808b03-3b7d-4b27-be2c-de3dad4bd5d6" />


kubectl get namespaces
kubectl get pods -A

<img width="442" height="242" alt="image" src="https://github.com/user-attachments/assets/68a452bb-9977-4b57-8074-e5d0b7182391" />

++++++++++++++++++++++++++++++++++++++++++++++++










