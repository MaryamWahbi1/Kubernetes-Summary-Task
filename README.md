# Kubernetes Summary Task
![](https://149695847.v2.pressablecdn.com/wp-content/uploads/2020/12/Kubernetes_AIM.jpg)
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

[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bit.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bit.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bit.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bit.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bit.PNG?raw=true")


- http://localhost/ynet

[![](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynet.PNG?raw=true)](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/ynet.PNG?raw=true)
------------

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
docker run -d -p 5000:5000 maryamwahbi/python-flask-ci:latest
```

[![https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true")](https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true "https://github.com/MaryamWahbi1/Kubernetes-Summary-Task/blob/master/screenshots/bitcoin_image.PNG?raw=true")


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















