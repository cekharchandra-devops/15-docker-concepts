FROM almalinux:9
ENV course="devops" \
    author="sekhar"\
    email="xyz.gmail.com"
RUN echo "course: $course, author: $author, email: $email"
CMD [ "sleep", "100" ]


# ARG is used to pass the values to the dockerfile from the command line. 
# it is similar to ENV but the values are not available in the container.
# values are only available during the build process.
# for ENV values are available in the container as well as during the build process.