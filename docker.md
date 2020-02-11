# Docker

This document is a quick reference guide to some of the basic and common commands used for Docker. You can view the official [Docker Documentation](https://docs.docker.com/engine/reference/run/) for more details. 

---------------
<br><br>

### Start A Docker Container
Start up a docker container. 
```cmd
docker-compose up -d
```
<br>

### Shut Down A Container
Stop a docker container.
```cmd
docker-compose down
```
<br>

### List All Containers
Run the following command to show a list of all active and inactive containers. 
```cmd
docker container ls -a
```
<br>

### Remove Container
Run the following command to remove a specific container
```cmd
docker container rm containerID // Replace containerID with the ID of the container that you would like to use
```
<br>

### Stop All Containers
Shut down all running containers.
```cmd
docker kill $(docker ps -q)
```
<br>

### Remove All Containers
Remove all containers.
```cmd
docker rm $(docker ps -a -q)
```
<br>

### Remove All Docker Images
Remove all docker images.
```cmd
docker rmi $(docker images -q)
```
<br>

### Removing All Unused Objects
This command will remove all stopped containers, images, and unused networks.
```cmd
docker system prune           // Removes all unused containers, images, and networks
docker system prune --volumes // Additionally removes unused volumes
```	
<br>

### Show All Non-Running Containers
Show a list of all stopped containers
```cmd
docker container ls -a --filter status=exited --filter status=created
```
<br>

### Copy Files From Docker Container
Use this function to copy files from within a docker container onto your local machine. 
```cmd
docker cp <container-id>:/path/to/container/files/ /local/machine/destination/
docker cp f1e1306559d7:/var/www/html/ ~/Desktop/DockerBAK/ // This is an example
```
