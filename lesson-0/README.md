## Listing your container

### running containers

`docker ps`

### all containers

`docker ps -all`

## Create a container

`docker create [imageName]`

> this gives us containerId

## Start a container

`docker start -a [containerId]`

-a = attach to the container and watch the output and give it back to the terminal

an alternative is to use logs

`docker logs [containerId]`

> `docker run` = `docker create` + `docker start`

## cleanup containers and cleanup disk space

`docker system prune`

To delete all containers including its volumes use

`docker rm -vf $(docker ps -a -q)`

## cleanup images

`docker rmi -f $(docker images -a -q)`

## stop container

`docker stop [conatinerId]` ideal choice

**SIGTERM** - if you need to shut down the container on its own time and little cleanup or action during that shutdown

In 10seconds if the container is not shutdown then docker issues SIGKILL to shut down immediately 

`docker kill [containId]`

**SIGKILL** - if you need to shut down the container the very instant(right now), and you don't get to do any cleanup or action during the shutdown

## running additional commands in a container

`docker exec -it [containerId] [command]`

## shell or command prompt within a container

`docker exec -it [containerId] sh`

`docker run -it [imageName] sh`

> Full terminal access. Used especially for debugging. To get out use `[ctrl + d]` or type `[exit]`.
