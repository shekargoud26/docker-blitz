# Containers

## Running docker containers

Docker containers can be run using the *docker client* running the ```docker run imagename:tag``` command.

- To list all the containers run or still running we use the ```docker ps -a ``` command.
- To run a docker container in detach mode (in background) we  add ```-d``` flag while running the container.
- To delete the container automatically after closing it we can add ```-rm``` flags while running the container.



## Docker inspect

Docker *inspect*  command displays low level information about a container or an image. 

Usage: 

```docker inspect container_id```



## Port mapping

- Ports of the container can be mapped to the ports of the host in order to communicate with the container.
- It can be done using the ```-p host_port:container_port``` flag and arguments while running the container using `docker run` command. 

## Docker logs

- The ```docker logs container_id``` command is used to view the console logs printed by the specified container.

## Docker container links

Docker containers link allow containers to securely transfer data from one container to another container.

**Example**:

Lets try to link our docker container with a redis container. 

First we start *redis* container in detached mode

```
docker run -d --name redis redis:3.2.0
```

Then we start our container from our docker image and mention `--link redis` argument to link it to redis(name specified while starting the container) container

```
docker run -d -p 5000:5000 --link redis myDockerImage:myTag
```

We can now access the redis server within our container using the hostname `redis` which docker will automatically resolve to the ip address of the redis container.