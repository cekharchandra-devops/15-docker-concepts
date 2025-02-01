FROM almalinux:9
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*
ONBUILD ADD index.html /usr/share/nginx/html/index.html
CMD [ "nginx", "-g", "daemon off;" ]

# ONBUILD instruction is used to execute the instruction 
# when the image is used as the base image.
# in the above case when the image is used as the base image, index.html must be present in the same directory.
# If the index.html is not present in the same directory, then the build will fail.
# base image owner can define the instruction to be executed when the image is used as the base image.
# it does not execute the instruction when the image is built.
# it executes the instruction when the image is used as the base image.