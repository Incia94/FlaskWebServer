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
