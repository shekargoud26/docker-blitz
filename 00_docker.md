# Docker

Docker is a tool that enables you to create, deploy, and manage  lightweight, stand-alone packages that contain everything needed to run  an application (code, libraries, runtime, system settings, and  dependencies). These packages are called containers.

Each  container is deployed with its own CPU, memory, block I/O, and network  resources, all without having to depend upon an individual kernel and  operating system. While it may be easiest to compare Docker and virtual  machines, they differ in the way they share or dedicate resources.



## Why docker?

1. **Reproducibility**: Similar to a Java application, which  will run exactly the same on any device capable of running a Java  Virtual Machine, a Docker container is guaranteed to be identical on any system that can run Docker. The exact specifications of a container are stored in a Dockerfile. By distributing this file among team members,  an organization can guarantee that all images built from the same  Dockerfile will function identically. In addition, having an environment that is constant and well-documented makes it easier to keep track of  your application and identify problems.

2. **Isolation**: Dependencies or settings within a container  will not affect any installations or configurations on your computer, or on any other containers that may be running. By using separate  containers for each component of an application (for example a web  server, front end, and database for hosting a web site), you can avoid  conflicting dependencies. You can also have multiple projects on a  single server without worrying about creating conflicts on your system.
3. **Environment Management**: Docker makes it easy to  maintain different versions of, for example, a website using nginx. You  can have a separate container for testing, development, and production  on the same server and easily deploy to each one.
4. **Continuous Integration**: Docker works well as part of  continuous integration pipelines with tools like Travis, Jenkins, and  Wercker. Every time your source code is updated, these tools can save  the new version as a Docker image, tag it with a version number and push to Docker Hub, then deploy it to production.
5. **Security**: With important caveats (discussed below),  separating the different components of a large application into  different containers can have security benefits: if one container is  compromised the others remain unaffected.