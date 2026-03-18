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









