FROM almalinux:9
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*
ADD https://raw.githubusercontent.com/cekharchandra-devops/15-docker-concepts/refs/heads/main/readme.MD /usr/share/nginx/html/index.html
RUN chmod +r /usr/share/nginx/html/index.html
CMD [ "nginx", "-g", "daemon off;" ]

# ADD instruction is used to copy files from the source to the destination.
# ADD instruction can also be used to copy files from the URL to the destination.
# ADD instruction can also be used to copy files from the source to the destination and also extract the tar file.
