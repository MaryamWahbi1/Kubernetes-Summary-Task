# Kubernetes Summary Task
## Explanation of the task:
1. Dockerize two applications:
 - YNET App: parses and presents the Breaking News XML in an HTML Table Format.
 - Bitcoin App: presents the Current BitCoin Price and presents the Average Price for the last 10 minutes.
2. Create Kubernetes manifests (Deployment and service)
3. Deploying apps - Minikube
4. Deploy/Enable Ingress Controller on cluster
5. Create an ingress that directs the traffic to the correct service:
http://.../ynet → ynet service
http://.../bitcoin → bitcoin service

------------


## Run the apps with Docker

##### Run Ynet image from DockerHub
```shell
docker pull maryamwahbi/ynet
docker run -d -p  8081:8081 maryamwahbi/ynet:latest
```
[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynetimage.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynetimage.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynetimage.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynetimage.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynetimage.PNG?raw=true")

##### Run Bitcoin image from DockerHub
```shell
docker pull maryamwahbi/python-flask-ci
docker run -d -p 8000:5000 maryamwahbi/python-flask-ci:latest
```

[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true")

------------


## Create Kubernetes manifests (Deployment and service)

- ##### YNET App

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: ynet 
  labels: 
    role: deployment

spec:
  replicas: 1
  
  selector:
    matchLabels:
      app: ynet

  template:
    metadata:
      labels:
        app: ynet
    spec:
      containers: 
      # The First Container
      - name: ynet
        image: maryamwahbi/ynet
        ports:
        - containerPort: 80
        env:
        - name: TITLE
          value: "Welcome to Ingress One" 
        - name: AUTHOR
          value: "Maryam Wahbi"
---
apiVersion: v1
kind: Service
metadata:
  name: ynet
spec:
  type: ClusterIP
  ports:
  - port: 80
  selector:
    app: ynet
```


- ##### Bitcoin App

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: bitcoin 
  labels: 
    role: deployment

spec:
  replicas: 1
  
  selector:
    matchLabels:
      app: bitcoin 

  template:
    metadata:
      labels:
        app: bitcoin 
    spec:
      containers: 
      # The First Container
      - name: bitcoin 
        image: maryamwahbi/python-flask-ci
        ports:
        - containerPort: 80
        env:
        - name: TITLE
          value: "Welcome to Ingress Two" 
        - name: AUTHOR
          value: "Maryam Wahbi"
---
apiVersion: v1
kind: Service
metadata:
  name: bitcoin 
spec:
  type: ClusterIP
  ports:
  - port: 80
  selector:
    app: bitcoin 
```

------------

## Run With Minikube

#### 1. Clone the project
```shell
git clone https://github.com/MaryamWahbi1/Kubernetes-Summary-Task.git
```
#### 2. Go to the project directory
```shell
cd Kubernetes-Summary-Task
```
#### 3. Start minikube
```shell
minikube start
```
#### 4. Enable ingress addons
```shell
minikube addons list
minikube addons enable ingress
```
[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/addons.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/addons.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/addons.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/addons.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/addons.PNG?raw=true")
#### 5. Namespaces - isolating groups
```shell
kubectl get po
kubectl get namespaces
kubectl -n ingress-nginx get po
```

#### 6. Apply Deployment
```shell
kubectl apply -f .
kubectl get po
kubectl get po,services
```
[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/apply.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/apply.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/apply.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/apply.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/apply.PNG?raw=true")

[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/getpo.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/getpo.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/getpo.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/getpo.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/getpo.PNG?raw=true")
#### 7. Start minikube tunnel
```shell
minikube tunnel
```
#### 8. Now, you can visit the websites using:
- http://localhost/bitcoin
- http://localhost/ynet

------------
### Delete Minikube
If you want to delete Minikube, run the following command:
```shell
minikube delete
```
------------
### Delete Deployment:
If you want to delete  deployment, run the following command:

```shell
kubectl delete --all po,deploy,svc,ingress,statefulset --force --grace-period 0

```















