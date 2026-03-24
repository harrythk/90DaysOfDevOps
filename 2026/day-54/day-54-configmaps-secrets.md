## Task 1: Create a ConfigMap from Literals

# Use kubectl create configmap with --from-literal to create a ConfigMap called app-config with keys APP_ENV=production, APP_DEBUG=false, and APP_PORT=8080
<img width="788" height="42" alt="image" src="https://github.com/user-attachments/assets/55bccc76-c383-4f4e-a19a-6f857284195a" />


# Inspect it with kubectl describe configmap app-config and kubectl get configmap app-config -o yaml

<img width="647" height="331" alt="image" src="https://github.com/user-attachments/assets/e2641d8f-c622-4bf7-9793-f3e9a1ecda16" />

<img width="665" height="171" alt="image" src="https://github.com/user-attachments/assets/929176be-ae60-4a55-98d6-73c85cd171ef" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Create a ConfigMap from a File

# Write a custom Nginx config file that adds a /health endpoint returning "healthy"
Create a ConfigMap from this file using kubectl create configmap nginx-config --from-file=default.conf=<your-file>
The key name (default.conf) becomes the filename when mounted into a Pod
