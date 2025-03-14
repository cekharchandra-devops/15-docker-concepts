# monolithic vs microservices:

Monolithic and microservices architectures are two different approaches to design and structure the applications.

when it comes to monolithic architecture,it is traditional approach where entire project is build, package as a single and indivisible unit includes (user interface, backend, data access layer interconnected each other) and the configuration required for running the application smoothly.

**characterstics:**

* Single Codebase: this means that the enitre applicaiton, including its various components and functionalities, is packaged and deployed as a single unit.
* common database: all the components uses same dabase
* Unified Deployment: Everything is deployed together, and any change requires redeploying the entire application.
* Tight Coupling: Different modules are interconnected and depend on each other within the application.

**pros:**

* entire project functionality at one place. easy to understand the design and development process.
* Monolithic applications can achieve high throughput and low latency as there is no inter-service communication overhead
* ensures data consistency with in single application.

**cons:**
* as project functionality increases, maintaining code as a single unit is quite challanging. change in part of application might effect on other part.
* specific component can't be scaled up. 
* uniform technology for entire application.
* deploying new features in a monolithic application can be complex. since entire application is deployed as single unit, any small change requires deploying entire application. there might be chance of deployment errors and downtime.
* an error in one component might bring down entire application.

**Microservice Architecuture**

in this approach, application is composed of loosely coupled, independently deployable services, each responsible for specific business function.

**pros:**
* as microservices are independently running services, it allows to scale based on load or demand
* option to choose best tech stack for particual business function. spring boot useful building service within less time where apache spark is suitable for running data intensive tasks.
* microservice promotes fault tolerance.as each microservice running independently, a failure of one service will not impact on entire echo system.

**cons:**
* requires more resources to maintain microservices based architecutre.
* quite challanging for data consistency across system.
* as each service interacts with others, there might be chance of performance issue due to network calls.   
* debugging and testing microservice based applications can be tough task.

# why docker / containerization:

***

***When a microservice architecture is chosen, the entire business functionality is designed and implemented as small, lightweight services that do not require high end servers to operate effectively.***


In the context of microservices architecture, Docker and containerization are particularly valuable because they align well with the core principles of microservices.

**isolation of services:**
* Microservices are designed to be independently deployable and manageable. Docker containers encapsulate each service along with its dependencies, ensuring it operates in isolation from other services. 

**Lightweight and Resource-Efficient**
* Microservices typically need to be lightweight to keep resource consumption minimal. Containers are less resource-intensive than virtual machines, enabling more efficient scaling and management of microservices without requiring "Bahubali" or powerful server configurations.

**Consistency Across Environments**
* Containers ensure that each microservice behaves consistently across different environments (development, testing, production), reducing the "it works on my machine" problem. This consistency is crucial in microservices, where multiple services need to interact reliably across various environments.

**Rapid Deployment and Scaling**
* Microservices benefit from the ability to quickly deploy, scale, and update individual services. Docker containers start up faster than traditional VM instances, making it easier to scale services up or down as needed in response to demand, which is ideal for high-performance microservices.

**Easy Automation with Orchestration Tools**

* In microservices, often deal with many small services. Container orchestration platforms like Kubernetes make it straightforward to manage these containers, automating deployment, scaling, and health checks. This enables microservices to operate smoothly in production with minimal manual intervention.

**Efficient Resource Utilization and Lower Costs**
* Containers enable optimal resource usage by packing multiple microservices on the same host without performance degradation. This reduces the need for high-powered servers, lowering infrastructure costs.

**physical servers vs VMs vs Containers**
* PENDING...


# docker installation on RHEL

**Set up the repository**

```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```

**To install latest version**
```
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**start docker**

```
sudo systemctl start docker
```
**add user to docker group to run docker command without root previledges**
```
usermod -aG <user-name> docker
```

**docker commands:**

***listed below commands are useful to pull the image from the repo and create container and run the container.***

```
docker ps (lists all running containers on that node)

docker ps -a (lists all the containers includes running and stopped)

docker images ( gives list images downloaded from the repository) 

docker pull nginx:version ( if it is vendor image) 

docker create nginx:version 

docker start container-id 

docker stop container-id 

docker rm container-id 

docker rm -f container-id( to stop forcefully and remove the container)

docker rmi image-id( to remove the image locally downloaded) 

docker run nginx ( it will pull the image from the repository if it not already exit in local repo and create the container and run the container) 

docker run -d nignx ( it runs the container in detaching mode) 

docker run -p 9090:80 nginx 

docker run -p 9091:80 nginx 

docker exec -it conatiner-id bash ( to login to container and opens the bash terminal) 

docker inspect <conatiner-id> ( gives information about container) 

docker logs <conatiner-id> ( gives the container logs) 

docker run -p 8080:80 --name docker-practice -d <conatiner-id> 
```

if nginx container is running inside the ec2 isntance, how to access the conatiner from outside the instance?
* container is like a nano server running inside the ec2 isntance. it also has (0-65535 ports) container opens 80 port on container. when user hits the request, it will reach to host port. we need to map host port with container port. using -p we can acheive this port forwarding docker run -p 80:80 nginx now, request will go through hostport to conatiner port and serve the request

**Customized docker images:**

***for every docker instruction, separate Dockerfile has been created for testing purpose.***

To build a custom Docker image, Docker provides the option to create a Dockerfile.
 
Dockerfile: this file is a declarative way of creating custom docker images. we can use docker instastruction to build the docker image.

FROM
-------
 
 FROM should be the first instruction in dockerfile. it represents base OS. there is an exception for ARG
```
 FROM <base-os> 
```
the base-os should be bare minimum OS unlike the the OS used in VMs (RHEL,Ubuntu)
So, almalinux almost similar to RHEL except that there is no support from the theam

how you build docker image?
```
docker build -t <image-name>:version .  
```
-t refers tag,  (.) refers current folder have Dockerfile file.

RUN
------

RUN instruction is used to configure image like installing packages, configure etc.` RUN instruction runs at the time of image building`.

CMD
-----

CMD instruction `runs at the time of container creation`. it keeps container running.

systemctl start nginx --> /etc/systemd/system/nginx.service

systemctl works only for full server. Starts the NGINX service as a background daemon managed by systemd.

ngnix -g daemon-off --> daemon-off instructs NGINX to run in the foreground instead of detaching to the background.

LABEL
----

it adds metadata to the image,  description , who is the owner, which projects, LABELS are used to filter the images.

EXPOSE INSTRUCTION DOESNT ACTUALLY PUBLISH THE PORT
------
used to let the users know what are the ports this container will open when it runs .

EXPOSE instruction will not effect functionality.it gives only information.

ENV
---
sets the environment varibles, these can be used inside container

COPY
-------
used to copy files from local to container

ADD
---
ADD also does same as COPY but it has 2 extra capabilities

1. it can get files from internet

2. it can extract the files into image.

ENTRYPOINT:
---
The ENTRYPOINT instruction in a Dockerfile specifies the main command that a container will execute when it starts.

1. CMD can be overridden at runtime.

2. you can't override ENTRYPOINT like CMD. if you try to do, it will go and append to the entrypoint command-name

3. for better result and best practices,CMD can provide the arguments to entrypoint. 
so you can mention default args through CMD and you can override them at run time.

USER:
---
for security reasons, conatiners should not run with root previledges, it must be on normal user. atleast last instruction should be USER.

WORKDIR:
---
workdir is used to set current working direcotry in docker image

ARG
---
ARG is used to set the variables at build time only, not inside the container

ARG vs ENV:
---

1 ENV variables can be access in` image build time and container run time both`.

2 ARG variables can only access at `the time of image creation`.

3 we can use ARG as` first instruction in Dockerfile before FORM in one spacecial case i.e to supply version to the base image`

4.ARG instruction `before FROM is only valid until FROM`. it cant be accessed after FROM
docker build -t args:v1 --build-arg course=docker .  --> we can override ARG variables using --build-arg 
 
how can we use ARG variable inside the container as well?
by setting value to ENV variable.

ONBUILD:
----------
ONBUILD is used to trigger few instructions at build time when user is using our built image.

docker commands:

```
docker ps --> running container
docker images --> gives images downloaded to local repo
docker pull <image>:version --> pulls the images to local repo

docker create <image>:version
docker start container-id
docker ps --> gives container info and status

docker run = docker create + docker start

docker stop container-id
docker rm conatiner-id
docker rm -f container-id

docker rmi image-id

docker run -d nginx:alpine-slim (run in detached mode)

docker container prune --> to remove only stopped containers
docker rm -f $(docker ps -aq) --> to remove all containers
docker rm -f `docker ps -aq` --> to remove all container (both are working fine)

docker ps -aq --> gives container id list (stopped and running)
docker images -aq --> gives list of images in our local

docker logs -f <container-id> --> shows container logs

docker exec -it bash/sh ==> to login to running container

docker run -d -p 8081:80 nginx:latest --> container runs on port 80 

docker build -t <image-name>:version

docker login -u <username>
password:

docker tag cmd:v1 cekharch/cmd:v1

docker push cekharch/cmd:v1

```


When you run the command: 

```
docker run -d -p 8081:80 nginx:latest
```
it maps the host port 8081 to the container port 80. Here's what happens internally:

1. Port Mapping
Host Port (8081): A port on your host system (your computer or server).
Container Port (80): A port inside the container where the Nginx service is listening.
Docker sets up port forwarding between these two ports. Any traffic sent to localhost:8081 on the host is forwarded to port 80 inside the container.

2. Internal Mechanism:

    a. **Network Namespace:** Each Docker container runs in its own network namespace, isolated from the host. Within this namespace, the container has its own virtual network interface and IP address.

    b. **Bridge Network:** By default, Docker containers are connected to a virtual bridge network (docker0 on Linux). This bridge allows communication between the host and the container.

    c. **iptables Rules:** Docker modifies the host's iptables (Linux firewall rules) to set up port forwarding. When you expose a port using -p, Docker adds rules to:

    * Forward traffic from the host port (8081) to the container's IP and port (e.g., 172.17.0.2:80).
    * Perform Network Address Translation (NAT) to rewrite the source and destination addresses.

For example:

```
Host (eth0:8081) --> Docker Bridge (docker0) --> Container (172.17.0.2:80)
```

d. **Service Listening** Inside the container, the Nginx server listens on port 80. The port mapping ensures that requests reaching localhost:8081 on the host are directed to port 80 in the container.



Docker Instructions:

FROM --> should be the first instruction to refer to the base os except ARG
RUN --> used to install packages and configure the images. this will execute at the time of image building
CMD --> executes at the time of container creation time.
EXPOSE --> it will give the metadata about which port the container is running on.
LEBEL --> helps to add key value pair to image metadata and helps to filter the iamges
COPY --> it will copy the files from source to destination
ADD --> it has two extra capabilities. it can copy the files to destination directly from internet locations and it can also copy tar files and extract it at destination location.

RUN VS CMD
ADD VS COPY
CMD vs ENTRYPOINT

