# Container & Docker 101

There are a few [valuable Docker](http://www.nkode.io/2014/08/24/valuable-docker-links.html) links out there.

## Placeholders
- $DCOS_CLI_HOME: DCOS command line tool directory
- $MASTER_IP_ADDRESS: Mesos Master IP address

## Install

Make sure you have your DCOS cluster per team up and running. Then do:

```
# get your team key
$ chmod 600 ~/.ssh/your-team-key
# add key once:
eval `ssh-agent -s`
ssh-add ~/.ssh/your-team-key
# log in with forwarding enabled (so that you can log in from master to one of the agents)
ssh -A core@$MASTER_IP_ADDRESS
```

We will carry out the following tasks on the Mesos master instance of the DCOS. It is a [CoreOS](https://coreos.com/) environment, so Docker native.

If you have issues sshing into the Master, check out https://docs.mesosphere.com/services/sshcluster/ or ask for help.

## Find Docker images

```
$ docker ps
$ docker images
$ docker search ubuntu
```

## Run Docker containers

```
$ docker run -t -i ubuntu:14.04 /bin/bash
# play around in the Ubuntu container and exit again
$ docker ps -a
$ docker images
```

## Run as daemon

```
$ docker run -d ubuntu:14.04 tail -f /dev/null
# note the container ID of your Ubuntu container
$ docker exec -it $CONTAINER_ID bash
$ docker pause $CONTAINER_ID
$ docker exec -it $CONTAINER_ID bash
$ docker unpause $CONTAINER_ID
```

## Kill a docker container
```
$ docker kill $CONTAINER_ID
$ docker ps -a
```

## Remove the container
```
$ docker rm $CONTAINER_ID
$ docker rm $(docker ps -aq)
```

## Remove the image
```
$ docker images
$ docker rmi <imageID>
```

## Pull an image
```
$ docker pull ubuntu
```
## Same as
```
$ docker pull ubuntu:latest
```

## Update an image
```
$ docker run -i -t ubuntu /bin/bash
    $ apt-get install -y git
$ docker ps -a
$ docker commit -m "added git" -a "janr" 3dac737f418c janr/ubuntu:v2
$ docker images
$ docker run -t -i janr/ubuntu:v2 /bin/bash
```

## Push to docker hub registry
## Requires user account
```
$ docker login
$ docker push janr/ubuntu:v2
```

## Build own image from Dockerfile
```
$ mkdir -p janr/nginx
$ cd janr/nginx
$ touch Dockerfile
```

## My Dockerfile
```
$ cat > Dockerfile <<EOF
FROM nginx
MAINTAINER Jan Repnak <jan.repnak@mesosphere.io>
RUN apt-get update && apt-get install -y git
RUN echo "I just built my first Docker image \o/" >> /usr/share/nginx/html/index.html
EOF

$ docker build -t janr/nginx:v2 .
$ docker run -d -p 8081:80 janr/nginx:v2
```

## Clean up Docker images and containers (should be run periodically)
```
$ docker rm -v $(docker ps -a -q -f status=exited)
$ docker rmi $(docker images -f "dangling=true" -q)
```
