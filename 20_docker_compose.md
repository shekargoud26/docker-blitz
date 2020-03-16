# Docker Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.



Using Compose is basically a three-step process:

1. Define your app’s environment with a `Dockerfile` so it can be reproduced anywhere.
2. Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated environment.
3. Run `docker-compose up` and Compose starts and runs your entire app.

A `docker-compose.yml` looks like this:

```yaml
version: '3'
services:
  dockerapp:
    build: .
    ports:
    - "5000:5000"
    depends_on:
    - redis
  redis:
    image: redis
```

Understanding the `docker-compose.yml` file

- We specify the Docker Compose version using the `version: '3'` variable. Here we are using version 3.
- Next we mention the `services` we want to run using *Docker Compose*. In our application there are two services *dockerapp(flask api)* and *redis server*.
- Within each service we mention the instructions for running that service. 
- The first instruction `build` instruction mentions the path that contains the *dockerfile* to be used for building the *dockerapp* image. 
- The second instruction is the `ports` instruction. Its similar to `-p` argument in docker client. The port format is `host_port:container_port`.
- Third instruction is `depends_on`. Docker compose will start services in dependency order mentioned in the depends_on section. Since we mention that our `dockerapp` depends on `redis` docker-compose will start `redis` first. 
- Since the `redis` official image is available we only mention the `image` instruction to specify which image to use. 

**Note: Version 2 docker compose has added a docker-network feature which allows a docker container to communicate with other container using it's name and hence we need not specify the link. **

Finally we can start the containers using `docker-compose up` command in the folder that contains the  `docker-compose.yml` file.