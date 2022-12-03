# Kubernetes Summary Task
## Explanation of the task:
1. Dockerize two applications:
 - YNET App: parses and presents the Breaking News XML in an HTML Table Format.
 - Bitcoin App: presents the Current BitCoin Price and presents the Average Price for the last 10 minutes.
2.  Create Kubernetes manifests (Deployment and service)
3. Deploy minikube
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
