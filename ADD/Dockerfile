FROM almalinux:9
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*
ADD https://raw.githubusercontent.com/cekharchandra-devops/15-docker-concepts/refs/heads/main/readme.MD /usr/share/nginx/html/index.html
CMD [ "nginx", "-g", "daemon off;" ]