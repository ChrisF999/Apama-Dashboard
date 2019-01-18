# Apama-Dashboard
Interaction Between Prometheus and Grafana

This Project is a Demo of how Apama can intract with Prometheus and though Prometheus then on to Grafana. 

It uses base stats built into Apama and stats that were made whilst runing a simple apama application.

## The docker continer will be enough for most people only use the the manual install if you have experience  with Apama, Prometheus and Grafana.

# DOCKER INSTALL INSTRUCTIONS

First a custom docker container must be made to hold Grafana with plugins there is a dockerfile that will containins that info for the build.
```
docker build -t grafana:latest-with-plugins (PATH TO FOLDER THAT CONTAINS THE DOCKERFILE)
```
The path ends in Apama-Dashboard\DockerContainer, make sure that the new container is called grafana:latest-with-plugins.

Next make sure that you are logged in with your docker store login and make sure that you have accsess to https://hub.docker.com/_/apama-correlator. 
Once you have logged in you will pull the correlator for apama.
```
docker pull store/softwareag/apama-correlator:10.3
```
Then you will have to deploy the stack. Make sure that you are in the directory where docker-compose.yaml is.
```
docker stack deploy -c docker-compose.yaml apamaProm
```

This deployment uses a random port selected for us by Docker, so you need to interrogate it to find the port your Docker host exposes for it.
```
docker service inspect apamaProm_grafana | grep PublishedPort
```
If you are on Windows you will either need to download and install grep or use this alternate method.
```
docker service ls
```
Then find the port from a window that looks like
```
vxmqhzd97p3k        apamaProm_grafana      replicated          1/1                 grafana:latest-with-plugins              *:30152->3000/tcp
```
So in this example the port is 30152.
From there connect to your docker host with the port that you have got via either of the two methods.
Then log in with the default Grafana login details :
* User: `admin`
* Password: `admin`