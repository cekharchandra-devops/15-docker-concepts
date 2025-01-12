FROM almalinux:9
RUN mkdir /tmp/docker
# RUN cd /tmp/docker
WORKDIR /tmp/docker
RUN echo "some content" > docker.txt
CMD [ "sleep", "100" ]

#  find / -iname "docker.txt"
# it actually copies the file to the root directory of the container
