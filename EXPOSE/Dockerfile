FROM almalinux:9
RUN dnf install -y nginx
EXPOSE 80
CMD [ "nginx", "-g", "daemon off;" ]
# EXPOSSSE instruction does not actually publish the port. 
# It functions as a type of documentation between the person who builds the image and the person who runs the container, about which ports are intended to be published.