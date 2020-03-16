# Docker networking

![image-20200316162150359](/home/shekar-android/Documents/0_My_Projects/docker-blitz/images/30_docker_network_model.png)

Docker uses networking capabilities of host system to provide networking for the containers. When docker daemon is installed a network interface *docker0* is created that bridges host network and container network. 

There are 4 types of docker networks

1. Closed netork
2. Bridge Network
3. Host Network
4. Overlay network



**NOTE**: Use the command `docker network ls` to see a list docker networks of networks created/being used on your host system. 

