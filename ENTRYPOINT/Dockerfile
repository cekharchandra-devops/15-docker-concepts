FROM almalinux:9
 CMD [  "google.com" ]
ENTRYPOINT [ "ping" ]


# CMD [ "ping", "google.com"] # CMD ARguments can be overridden from directly docker commands

# ENTRYPOINT [ "ping", "google.com" ]
# docker run -d <image-name>: version ping yahoo.com
# this will actually append to existing entrypoint command

# ENTRYPOINT [ "ping" ] we cant override the entrypoint command

# but by using CMD and ENTRYPOINT together we can override the entrypoint command for better results.
