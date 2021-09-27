# FlaskWebServer
Basic WebServer in Python Flask with Public Docker Image and Kubernetes Manifest

Prerequisites -
Flask (sudo apt-get install flask) 
Linux (This docker image was buit and run on top of Linux Ubuntu with Docker installed on it)


The Repo has the following files -

main.py -

This file is a WebServer written in Flask Python which returns the output as teh following json -

{
  "timestamp": "<current date and time>",
  "ip": "<the IP address of the visitor>"
}

![snip](https://user-images.githubusercontent.com/38821348/134876967-db0b8298-985a-41b4-839a-ddfc211c2d15.JPG)
  

Requirements.txt -
It is a file which contains dependencies required while Building Dockerfile

  
Dockerfile -
This is a dockerfile configuration which is built to obtain the docker image
  
Manifest.yaml
  
This is a K8s mainfest which can be applied on top of a k8s cluster using -
  
kubectl apply -f Manifest.yaml


STEPS -
  1. Created a Folder WebServer with main.py and requirements.txt inside a Linux VM with Docker installed previously
  2. Created a Dockerfile
  3. Build a Docker image using the following command -
     docker login
     docker build --tag incia123/flask-web-server:webserver .
  4. Push the image to Docker hub using -
     docker push  incia123/flask-web-server:webserver
  5. We can Run the codker image directly in the local environment as follows -
     docker run webserver
  6. To get the Web Output in the terminal use the follwing command -
     curl http://<Expose-IP>:5000
  7. Once the docker image is uploaded to the dockerhub pubilc repo , it can be used to create a kubernetes deployment in an existing deployment of K8s
     kubectl -n <namespace> create deployment incia --image=incia123/flask-web-server:webserver
     kubectl expose deployment incia --type=LoadBalancer --port=5000 --target-port=5000 -n <namespace>
  8. Go to kubectl -n <> get svc | grep incia which exposes the Loadbalancer IP which can be used to access the WebServer from any browser irrespective of the OS.
  9. The other way we can deploy to kubernetes is directly using the kubectl apply -f Manifest.yaml with specifications for K8s deployment and service.
