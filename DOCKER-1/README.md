# Docker Image Save and Load Commands

## Saving a Docker Image
 command `docker save -o node-image.tar node:latest`

## Loading a Docker Image
command `docker load -i node-image.tar` 

# Edit Inside nginx Container
'1-docker build ID-IMAGE
 2-docker run -d -p ID-CONTAINER
 3-docker exec  ID-CONTAINER bash
 4-cd FILES IMAGE 
 5- EDIT'

# run image with more ports
'docker run -d \
  -p 8080:80 \
  -p 8443:443 \
  IMAGE-NAME'

# run image with random ports 
  'docker run -d \
  -p 80 \
  -p 443 \
  IMAGE-NAME'

 
