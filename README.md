#jAER - Java tools for AER


## Install

1- Check out the code

```
git clone git@github.com:cocheok/jaer_docker.git
```

2- Build the docker image using the following command

```
  docker build -t dvs .
```

   We can check that the image exist using the following command

```
  docker images dvs
```


3- Then we can create the container of the dvs image using the following command:

```
docker run -d -t -it --name dvs_container --net host -v ./data:/data --privileged -e DISPLAY=$DISPLAY dvs
```

Or we can create the container of the dvs image as a docker-compose service using the following command:

```
docker-compose up
```
