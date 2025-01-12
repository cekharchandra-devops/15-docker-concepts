ARG version
FROM almalinux:${version:-10}
ARG course="devops" \
    author="sekhar"\
    email="xyz.gmail.com"
RUN echo "course: $course, author: $author, email: $email"
CMD [ "sleep", "100" ]


# ARG is used to pass values to image during the build process. 
# it is similar to ENV but the values are not available during the container runtime.
# values are only available during the build process.
# for ENV values are available in the container as well as during the build process.
# docker build -t arg:v1 --build-arg course=aws .
# we can override the default values of ARG during the build process.

# we can also use AGRS in the FROM instruction.