# Docker Image Save and Load Commands

## Saving a Docker Image
 command `docker save -o node-image.tar node:latest`

## Loading a Docker Image
command `docker load -i node-image.tar` 

# Edit Inside nginx Container
 command docker build ID-IMAGE
 command docker run -d -p ID-CONTAINER
 command docker exec  ID-CONTAINER bash
 command cd FILES IMAGE 
 command EDIT

# run image with more ports
command docker run -d \
  -p 8080:80 \
  -p 8443:443 \
  IMAGE-NAME

# run image with random ports 
 command docker run -d \
  -p 80 \
  -p 443 \
  IMAGE-NAME

 
