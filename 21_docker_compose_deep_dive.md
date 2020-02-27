# Deep dive into Docker compose workflow

## Useful commands

- docker-compose workflow starts with `docker-compose up` command.
- `docker-compose up -d` command to run the process in the background.
- `docker-compose ps` command can be used to check the status of the containers manages by docker-compose.
- `docker-compose logs ` view the logs of the compose managed containers. `-f `to append new logs to the console. 
- We can use `docker-compose stop` command to stop all the compose manages containers without removing them. We can restart all the stopped containers by running `docker-compose up` or `docker-compose start`.
- `docker-compose rm` removes all the containers. 

## Re-building images

- when you run `docker-compose up` it will first look if the images are already present and starts containers using them. In case if you make changes to a `dockerfile`  and re run the `docker-compose up` command it will still run the containers from the previos images. 
- To force rebuild docker images we use `docker-compose build` command to force rebuild images for all the modified dockerfiles and then  `docker-compose up` to start the containers from the new images.

TL;DR: Always use `docker-compose build` everytime you modify a dockerfile. 

