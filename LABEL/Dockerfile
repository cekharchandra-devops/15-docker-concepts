FROM almalinux:9
RUN dnf install nginx -y
LABEL maintainer="sekhar" \
        version="1.0" \
        description="This is a sample Dockerfile with LABEL instruction"
CMD [ "nginx", "-g", "daemon off;" ]
# The LABEL instruction is used to add metadata to the image.
# it helps to identify the image and its properties using filters.
# docker images -f 'label=maintainer=sekhar'
