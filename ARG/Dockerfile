ARG version
FROM almalinux:${version:-9}
ARG course="devops" \
    author="sekhar"\
    email="xyz.gmail.com"
RUN echo "course: $course, author: $author, email: $email, version: $version"
CMD [ "sleep", "100" ]


# ARG is used to pass values to image during the build process. 
# it is similar to ENV but the values are not available during the container runtime.
# values are only available during the build process.
# for ENV values are available in the container as well as during the build process.
# docker build -t arg:v1 --build-arg course=aws .
# we can override the default values of ARG during the build process.

# we can also use AGRS before the FROM instruction. see the above example. 
# version is passed to the image during the build process.

#  docker build -t arg:v1 --build-arg version=8 .

# ARG as a first instruction in the Dockerfile is valid only for FROM isntruction.
# if we use ARG after FROM instruction, then it is not valid for any other instruction in the Dockerfile.