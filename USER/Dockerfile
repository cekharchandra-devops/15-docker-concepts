FROM almalinux:9
RUN usradd expense
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*
ADD https://raw.githubusercontent.com/cekharchandra-devops/15-docker-concepts/refs/heads/main/readme.MD /usr/share/nginx/html/index.html
RUN chmod +r /usr/share/nginx/html/index.html
USER expense
CMD [ "nginx", "-g", "daemon off;" ]

# always recommended to use the USER instruction to run the container as a non-root user.
# The USER instruction is used to set the user name or UID to use when running the image and for any RUN, CMD, and ENTRYPOINT instructions that follow it in the Dockerfile.
# otherwise, the container will run as a root user by default. that will be a security risk.
# atleast, the last instruction in the Dockerfile should be the USER instruction.
