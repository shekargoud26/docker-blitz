# Dockerfile instructions

Here we discuss some best practices for writing *Dockerfiles*.  

## RUN

- Split long or complex `RUN` statements on multiple lines separated with backslashes to make your `Dockerfile` more readable, understandable, and maintainable.
- Each **RUN** instructions will execute the command on the top writable layer of the container, then commit the container as a new image.
- The new image is used for the next step in the *Dockerfile*. So each **RUN** instruction will create a new image layer. 
- It is recomended to chain the **RUN** instructions in the *Dockerfile* to reduce the number of image layers it creates



**Example**:

**File 1**

```
FROM debian:jessie
RUN apt-get update
RUN apt-get install vim -y
RUN apt-get install git -y
```

**File 2**

```
FROM debian:jessie
RUN apt-get update && apt-get install vim git -y
```



Here the **File 1** will create three layers above the base layer while  **File 2** will create only one layer above the base layer.



## ENV 

To make new software easier to run, you can use `ENV` to update the `PATH` environment variable for the software your container installs. For example, `ENV PATH /usr/local/nginx/bin:$PATH` ensures that `CMD ["nginx"]` just works.



The `ENV` instruction is also useful for providing required environment variables specific to services you wish to containerize, such as Nvidia’s `NVIDIA_VISIBLE_DEVICES`.

## FROM

Whenever possible, use current official images as the basis for your images. We recommend the [Alpine image](https://hub.docker.com/_/alpine/) as it is tightly controlled and small in size (currently under 5 MB), while still being a full Linux distribution.



