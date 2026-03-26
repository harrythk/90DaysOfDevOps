# Task 1: Create a ConfigMap from Literals

## Use kubectl create configmap with --from-literal to create a ConfigMap called app-config with keys APP_ENV=production, APP_DEBUG=false, and APP_PORT=8080
<img width="788" height="42" alt="image" src="https://github.com/user-attachments/assets/55bccc76-c383-4f4e-a19a-6f857284195a" />


## Inspect it with kubectl describe configmap app-config and kubectl get configmap app-config -o yaml

<img width="647" height="331" alt="image" src="https://github.com/user-attachments/assets/e2641d8f-c622-4bf7-9793-f3e9a1ecda16" />

<img width="665" height="171" alt="image" src="https://github.com/user-attachments/assets/929176be-ae60-4a55-98d6-73c85cd171ef" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Create a ConfigMap from a File

## Write a custom Nginx config file that adds a /health endpoint returning "healthy"
## Create a ConfigMap from this file using kubectl create configmap nginx-config --from-file=default.conf=<your-file>
The key name (default.conf) becomes the filename when mounted into a Pod

<img width="779" height="47" alt="image" src="https://github.com/user-attachments/assets/b1e3da1d-bd22-4f18-aa7b-30487a46dbd8" />

<img width="1324" height="642" alt="image" src="https://github.com/user-attachments/assets/23466fc3-0917-424b-8da1-239a294fafdc" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Use ConfigMaps in a Pod
## Write a Pod manifest that uses envFrom with configMapRef to inject all keys from app-config as environment variables. Use a busybox container that prints the values.

apiVersion: v1
kind: Pod
metadata:
  name: hello
spec:
      containers:
      - name: hello
        image: busybox
        command:
          - /bin/sh
          - -c
          - |
            echo "APP_ENV=$APP_ENV"
            echo "APP_DEBUG=$APP_DEBUG"
            echo "APP_PORT=$APP_PORT"
            sleep 3600
        envFrom:
          - configMapRef:
              name: app-config 

<img width="1181" height="242" alt="image" src="https://github.com/user-attachments/assets/96685df2-1b8a-474a-a9cf-189178ea252a" />

## Write a second Pod manifest that mounts nginx-config as a volume at /etc/nginx/conf.d. Use the nginx image.

apiVersion: v1
kind: Pod
metadata:
  name: nginx-health
spec:
      containers:
      - name: nginx-health
        image: nginx:latest
        ports:
          - containerPort: 80
        volumeMounts:
          - name: nginx-config-storage
            mountPath: /etc/nginx/conf.d
      volumes:
        - name: nginx-config-storage
          configMap:
            name: nginx-config

## Test that the mounted config works: kubectl exec <pod> -- curl -s http://localhost/health

<img width="461" height="29" alt="image" src="https://github.com/user-attachments/assets/5402bc6b-e9ba-4574-ad49-9dcaf120150c" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


# Task 4: Create a Secret

## Use kubectl create secret generic db-credentials with --from-literal to store DB_USER=admin and DB_PASSWORD=s3cureP@ssw0rd
## Inspect with kubectl get secret db-credentials -o yaml — the values are base64-encoded
## Decode a value: echo '<base64-value>' | base64 --decode

<img width="373" height="199" alt="image" src="https://github.com/user-attachments/assets/60306e12-d0d7-436e-ab46-26b3f3b9627b" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


# Task 5: Use Secrets in a Pod










