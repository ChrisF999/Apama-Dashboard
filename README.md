# Apama-Dashboard
Interaction Between Prometheus and Grafana
This Project is a Demo of how Apama can intract with Prometheus and Grafana. 
It useses base stats built into Apama and stats that were made whilst runing a simple apama application.

# DOCKER INSTALL INSTRUCTIONS

Fisrt A custom dockercontainer must be made to hold Grafana with plugins there is a dockerfile that will containins that info for the build.
```
docker build -t grafana:latest-with-plugins (PATH TO FOLDER THAT CONTAINS THE DOCKERFILE)
```
The path ends in Apama-Dashboard\DockerContainer, make sure that the new container is called grafana:latest-with-plugins.

Next make sure that you are logged in with your docker store login and make sure that you have accsess to https://hub.docker.com/_/apama-correlator. 
Once you have logged in you will pull the corrilator for apama.
```
docker pull store/softwareag/apama-correlator:10.3
```
Then you will have to deploy the stack. Make sure that you are in the diracorty where docker-compose.yaml is.
```
docker stack deploy -c docker-compose.yaml apamaProm
```

This deployment uses a random port selected for us by Docker, so you need to interrogate it to find the port it will be available on your Docker host.
```
docker service inspect prometheus_grafana | grep PublishedPort
```
If you are on windows you will either need to download and install grep or use this alteanate methord.
```
docker service ls
```
Then find the port from a window that looks like
```
vxmqhzd97p3k        apamaProm_grafana      replicated          1/1                 grafana:latest-with-plugins              *:30152->3000/tcp
```
So in this exsaple the port is 30152.
From there connect to your docker hoast with the port that you have got via either of the two methords.
Then log in with the defult Grafana login details, User admin, password admin. 