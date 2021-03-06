# This is actually a Docker Lab

The purpose is to:

1. Create Docker image FROM scratch

2. Introduce Multi-Stage Builds.

The helloworld.go provides a simple web server that says Hello World.

The Dockerfile creates a Docker image from scratch and places the Hello World web server inside it.

Steps: (Suppose you have Docker Engine on Linux or Docker Desktop on your Mac)

```
# docker pull golang

# docker run -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):$(which docker) -it golang /bin/bash

## Now we are inside of golang container, run following build command to generate static executable

root@af3e87a15727:/go# CGO_ENABLED=0 go get -a -ldflags '-s' github.com/jefff-guu/Docker_Lab
root@af3e87a15727:/go# mv $GOPATH/bin/Docker_Lab $GOPATH/bin/helloworld
root@af3e87a15727:/go# ldd $GOPATH/bin/helloworld                                                
   not a dynamic executable

root@af3e87a15727:/go# cp $GOPATH/src/github.com/jefff-guu/Docker_Lab/Dockerfile $GOPATH

root@af3e87a15727:/go# docker build -t jeff/helloworld $GOPATH

# Exit golang container and go back to Mac


Outside the container, you can run following command to start the container on your Mac and open a browser to verify it.
# docker run -it --name helloword -p 8080:8080 jeff/helloworld
```