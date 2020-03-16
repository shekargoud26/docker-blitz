# Bridge Network

This is the default type of networks in docker containers. All the containers in the same bridge network are connected to each other and they can connect to the outside world using the bridge interface. 

![image-20200316162150359](/home/shekar-android/Documents/0_My_Projects/docker-blitz/images/30_docker_network_model.png)

When docker daemon is installed it creates a default `bridge` network interface that can be seen using `docker network ls` command and inspected using `docker inspect bridge` command. 



## Running a bridged container

1. Lets create a container in using bridge network

```
docker run -it --name container_1 busybox
```

once the container starts use `ifconfig` to display the network interfaces.

```
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:40 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:6264 (6.1 KiB)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

```

The IP range of the container is 172.17.0.0 - 172.17.255.255. 

2. Lets create another container in using bridge network

```
docker run -it --name container_2 busybox
```

let's check the network interfaces of this container

```
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:03  
          inet addr:172.17.0.3  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:41 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:6364 (6.2 KiB)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

We can see the the IP for the new container is within the IP range mentioned earlier.



3. We can ping container_1 from container_2 to check if they're connected

   ```
   PING 172.17.0.2 (172.17.0.2): 56 data bytes
   64 bytes from 172.17.0.2: seq=0 ttl=64 time=0.128 ms
   64 bytes from 172.17.0.2: seq=1 ttl=64 time=0.178 ms
   ```

   

## Creating custom bridges

By default different bridge networks are isolated to each other. Only containers within the same bridge network can communicate with each other. The containers created previosly use the default `bridge` network created by the docker daemon and hence can communicate with each other. 



- Use this command to create a new bridge network

```
docker network create --driver bridge my_bridge_net
```

- Use `docker network ls` command to see if its created.
- Use command `docker inspect my_bridge_net` to see more details about it.

```
[
    {
        "Name": "my_bridge_net",
        "Id": "72c3809f307e7ff9c6aa67161fe8117da3a7ee5c4d18c2e68d2c1e0528af1a65",
        "Created": "2020-03-16T17:00:12.428597899+05:30",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.21.0.0/16",
                    "Gateway": "172.21.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
```



## Creating containers with custom bridge

We can specify the bridge network to be used by the container while running it using the `--net` tag. 

```
docker run -it --net my_bridge_net --name container_3 busybox
```

lets check the IP address of the new container using `ifconfig`

```
eth0      Link encap:Ethernet  HWaddr 02:42:AC:15:00:02  
          inet addr:172.21.0.2  Bcast:172.21.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:37 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:5918 (5.7 KiB)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

As we can see the new IP address is in within the range of the new bridge network (172.21.0.0\24)  



Since *container_3* is in a different network compared to *container_1* and *container_2* we cant ping container 1 and 2 from *container_3*.  



## Connecting bridges

We use the following command to connect a container from one bridge network to another bridge network. 

```
docker network connect bridge container_3
```

here the *bridge* is the network interface to which *container_3* has to be connected/bridged. 