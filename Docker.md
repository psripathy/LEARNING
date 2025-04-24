## Intro to Docker

[#LearnDocker | Docker](https://www.docker.com/101-tutorial)

[Graduated and incubating projects | Cloud Native Computing Foundation (cncf.io)](https://www.cncf.io/projects/)

|                    Virtual Machines (VMs)                    |                          Containers                          |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![Screen-Shot-2018-03-20-at-9.24.09-AM](https://www.netapp.com/media/Screen-Shot-2018-03-20-at-9.24.09-AM_tcm19-56643.png?v=85344) | ![Screen-Shot-2018-03-20-at-9.24.09-AM](https://www.netapp.com/media/Screen-Shot-2018-03-20-at-9.24.09-AM_tcm19-56643.png?v=85344) |



##### <u>Containerization</u>

- Containers share same OS Kernel as host
- Containers supports only Linux
- Container performance is greater than Linux



##### <u>Container Image</u>

When running a container, it uses an isolated filesystem. This custom filesystem is provided by a **container image**. Since the image contains the container's filesystem, it must contain everything needed to run an application - all dependencies, configuration, scripts, binaries, etc. The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata



##### <u>Containerization Technologies</u>

Two major Kinds: [Linux Containers Vs Docker](https://www.section.io/engineering-education/lxc-vs-docker-what-is-the-difference-and-why-docker-is-better/)

|                 Linux Containerization (LXC)                 |                            Docker                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| Focuses on OS Containerization. LXC is multi-purpose operating system virtualization. | Thrives on Application Containerization. Docker is single-purpose application virtualization |
| Fully functional OS environment that you can SSH into and operate it as an OS and install any application/services | Each instance of a container runs one process (application)  |
|                    Can run only on Linux                     | Runs natively on Linux, but not entirely dependant on Linux. Supports Windows/Mac OS |
| ![LXC container](https://www.section.io/engineering-education/lxc-vs-docker-what-is-the-difference-and-why-docker-is-better/lxc-container.png) | ![A Docker container](https://www.section.io/engineering-education/lxc-vs-docker-what-is-the-difference-and-why-docker-is-better/a-docker-container.png) |



##### <u>Docker Engine Components</u>

Docker Daemon :  Provides persistent background process that manages other docker components (like container, images, network, storage volumes)

Docker Engine API: Powered by REST. Used by app developers to communicate with docker

Docker CLI: Can setup a container, bind it with a volume, expose it at a particular IP or configure virtual networks.

Registry: Repository of docker images



##### <u>Docker on AWS</u>

- Amazon ECS (Elastic Container Service) - Fully Managed Container orchestration service for running docker containers on AWS. You have to maintain the EC2 instances.
- AWS Fargate - Technology you can use with Amazon ECS to run containers without having to manage infrastructure.
- Amazon EKS (Elastic Kubernetes Service) - Managed Container service to run and scale Kubernetes applications.
- Amazon ECR (Elastic Container Registry) - Fully managed Container registry to store images.



##### <u>Docker Data Persistence</u>

![image-20211117151000668](/Users/sxp002/Library/Application Support/typora-user-images/image-20211117151000668.png)

- Volumes provide the ability to connect specific filesystem paths of the container back to host machine.
- Data Volumes can be shared among containers. Volumes exist by default and stay even if the containers are deleted.
- Volume Types: Named Volumes, Bind Mounts, SFTP, Ceph, NetApp, S3 and more
- Create Named Volume: **docker volume create <volume_name>**
- Mount a volume in the container: **docker run -dp <in_port>:<out_port> -v <volume_name>:<file_path_in_container> <image_name>** -d runs the container in detached mode, -p is for port mapping
- Volume location on host machine: **docker volume inspect <volume_name>**
- Bind mounts are mounted into running containers and is often used to provide additional data into containers
- TMPFS (actually from memory), but appear as mounted file system within the container. Volatile - meaning gets deleted when the container is deleted
- Named pipes - Used to build communication between host and container.

|                                              |           Named Volumes            |            Bind Mounts            |
| -------------------------------------------- | :--------------------------------: | :-------------------------------: |
| Host Location                                |           Docker chooses           |            You control            |
| Mount example                                | Volume_name:/path/inside/container | /host/path:/path/inside/container |
| Populates new volume with container contents |                Yes                 |                No                 |
| Supports Volume drives                       |                Yes                 |                No                 |



##### <u>Container Networking Models (CNM)</u>

1. Network Sandbox will contain Container and the container will have an app Endpoint.
2. The endpoint will will build a Network. This network within the container will be intercepted by Docker Engine.
3. The Docker Engine will use 2 drivers (Network Driver & IPAM driver) to connect with underlying host network infrastructure.
4. ![image-20211117152454839](/Users/sxp002/Library/Application Support/typora-user-images/image-20211117152454839.png)



##### <u>DockerImage Architecture</u>

4 important parts

1. Index (manifest list. 1 to many manifest list)
2. Every manifest relate to a configuration
3. Each configuration has a multiple layers
4. Root file system (linux style) on top of the configuration/layers

![image-20211117153716677](/Users/sxp002/Library/Application Support/typora-user-images/image-20211117153716677.png)



##### <u>DockerFile</u>

The Dockerfile is essentially the build instructions to build the image.

1. **ADD** - Copy new files/directories/*<u>remote file URL</u>* and add them to the Docker Image specified as destination

2. **ENTRYPOINT** - Allows to configure a container that will run as an executable

3. **COPY** - Copies files/directories to the file system of the Docker Image (Same as 'ADD', but without the tar and remote URL handling)

4. **ENV** - Environment variable

5. **EXPOSE** - When specified allows the container to listen on a certain port. We can specify both TCP/UDP as communication protocol. TCP is the default

6. **FROM** - Specify the base image for the current image

7. **LABEL** - Instruction that adds metadata to the image

8. **STOPSIGNAL** - Instructs the container to exit

9. **USER** - Sets the user name & group when running an image

10. **VOLUME** - Manage data

11. **WORKDIR** - Sets the working dir for entry point, add or copy

    

##### <u>Docker Commands</u>

- Build a Container Image: ***docker build -t <image-name> .***
- Start/Run a Container: ***docker run -dp 3000:3000 <image-name>***
- Start/Run a Container while using docker-compose: ***docker-compose up -d***
- Get Container ID: ***docker ps***
- Stop the Container: ***docker stop <the-container-id>***
- Stop the Container while using docker-compose: ***docker-compose down***
- Remove the Container: ***docker rm <the-container-id>***
- Push Image to Registry: ***docker push docker/<image-name>***
- Tag Image: ***docker tag <tag-name> YOUR-USER-NAME/<image-name>***
- Execute a command inside Docker Container: ***docker exec <container-id> cat /data.txt***
- Create Volume: ***docker volume create <volume-name>***
- Inspect a Volume: ***docker volume inspect <volume-name>***
- Docker Logs: ***docker logs -f <container-id>***
- Create network: ***docker network create <network-name>***
- Run a Docker Container in a network: ***docker run -d --network <network-name> --network-alias <network-alias>  -v todo-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=todos mysql:5.7***
- Scan Image: ***docker scan <image-name>***
- Ignore files to be copied when building docker image - Use ***.dockerignore*** file
- [Execute command on host from docker container](https://stackoverflow.com/questions/32163955/how-to-run-shell-script-on-host-from-docker-container)
- Extract docker image 
    
    docker create --name="tmp_$$" image:tag
    
    docker export tmp_$$ > img.tar
    
    tar -xf img.tar
    
    docker rm tmp_$$

- Run docker image in interactive mode
     docker run -it --user <uid> <imageid> /bin/bash

- Step into running dicker container
  docker exec -it --user <uid> <container-id> /bin/bash
    
