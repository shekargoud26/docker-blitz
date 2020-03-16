# None Network

This network has no access to the network. In *None Network* 

the container used to containerize our application lacks a network layer. This kind of container is also called as a *closed container*. 



To start a container using *None Network* we use `--net` tag

example: 

```docker run -it --net none busybox ```

Once you run the above command and start the busybox container, you can use `ifconfig` command to see that there are no network interfaces other than a *loopback* interface. 

```
lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```



## Pros

- Provides maximum level of network protection

## Cons

- Not a good choice if network or internet connection is required

