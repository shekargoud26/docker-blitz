# Define Container Networks with Docker Compose

We can define and specify network bridges to be used by containers in the `docker-compose.yml` file using the `networks` tag. 



```dockerfile
version: '3'
services:
  dockerapp:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - redis
    networks:
      - my_net
  redis:
    image: redis
    networks:
      - my_net
networks:
  my_net:
    driver: bridge

```



Here we define a new bridge network using the `networks` identifier.  We also use `networks` identifier to mention the network to be used by the containers.

 