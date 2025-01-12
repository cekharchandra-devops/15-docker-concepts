FROM almalinux:9
RUN dnf install -y httpd \
    nginx 
    
# it is possible to run multiple commands in a single RUN instruction.  
# This is useful for reducing the number of layers in the image.
# The following example shows how to install multiple packages in a single RUN instruction:
# RUN dnf install -y httpd \
#     php \
#     php-mysql
# this instruction will be executed at the time of building the image
# CMD instruction will be executed at
# the time of running the container from the image  