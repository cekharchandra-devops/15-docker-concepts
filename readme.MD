# Docker installation steps:

run below commands with root access.

```
dnf -y install dnf-plugins-core
dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
systemctl enable --now docker
usermod -aG docker ec2-user
```

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

