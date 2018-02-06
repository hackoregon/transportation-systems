# Quick Guide to Docker Troubleshooting

## Assumptions
1. You have Docker hosting working.
2. You have a `docker-compose.yml` file, some Dockerfiles, and have tried starting the services via `docker-compose up -d`. 
The `docker-compose up -d` has listed some containers. Now what?

## Container status
Type `docker ps` at the host command line. 
You should see all the containers the `docker-compose up -d` said it started. 
If not, one or more of them probably crashed.

Type `docker ps -a`. This will list the containers that are running and the ones that have crashed.

## Container logs
From the `docker ps` you can see the container names. 
Type `docker logs <container-name>`, where `<container-name>` is the name of the container. 
If you want to follow a container's logs as it creates them, type `docker logs -f <container-name>`.

## Getting a `root` console
Type `docker exec -it -u root <container-name> /bin/bash`. You'll be on a virtual console in the container as `root`.
It's probably Debian Linux; the containers we're building for Transportation are built on Debian.
But there aren't many conveniences. There's probably not a text editor, man pages or other goodies. 
But if you want to use something and it's not there, you can install it!

For example - you want `vim` - type `apt update && apt-install vim-nox`. Now you have `vim`! 
`man` pages? `apt update && apt install man-db && mandb`.

You type a command and it's not there. Worse yet, you don't know what Debian package it's in! 
Type `apt update && apt-install apt-file && apt-file update`. 
Now type `apt-file search <missing-command>` and `apt-file` will list the packages that match the string!
