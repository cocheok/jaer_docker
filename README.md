#DVS 128

## Install


Create the Dockerfile file with the following content.

### Dockerfile
´´´
FROM java:7
RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install udev
RUN apt-get install subversion
ADD ./rules/65-inilabs.rules /etc/udev/rules.d/65-inilabs.rules
ADD ./rules/66-inilabs_dev.rules /etc/udev/rules.d/66-inilabs_dev.rules
RUN cd /usr/src/
RUN svn checkout https://svn.code.sf.net/p/jaer/code
WORKDIR /usr/src/code/jAER/trunk/
CMD ["udevadm control --reload"]
´´´

We can build the image using the following command
´´´
docker build -t dvs .
´´´



Then we can create the container with the following command:
´´´
docker run -d -t -it --name dvs_container --net host -v ./data:/data --privileged -e DISPLAY=$DISPLAY dvs

´´´

To create the container as a service we can use docker-compose.yml:

### docker-compose.yml

´´´
version: '2'

services:
  dvs:
    image: dvs2
    volumes:
      - ./data:/data
    environment:
      - DISPLAY=$DISPLAY
    network_mode: "host"
    privileged: true

´´´

To run the docker-compose

´´´
docker-compose up
´´´
