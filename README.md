Lychee Dockerfile
=============

This repository contains Dockerfile of Lychee for Docker's automated build published to the public Docker Hub Registry.

# Credits
This was forked from kdelfour/lychee-docker, and I based it off of his build file.  
Please check out his repository [kdelfour/lychee-docker](https://github.com/kdelfour/lychee-docker).

I also used bobmaerten's Dockerfile at [bobmaerten/docker-wallabag](https://github.com/bobmaerten/docker-wallabag) as a basis for switching the base to phusion/baseimage.

# Image Details
- This image is based on kdelfour/lychee-docker, but the base was switched to phusion/baseimage-docker from dockerfile/supervisor (which has been deprecated).  
- This image does **not** include mysql.  You will have to point it to an external or linked mysql server.  
- If you would like a version with mysql built in please check out kdelfour's version.  You can find it in his repository here: [kdelfour/lychee-docker](https://github.com/kdelfour/lychee-docker).  
- You should probably map the exposed /uploads and /data to directories outside the container for data persistence.  [Check here for suggestions on how to do that](https://docs.docker.com/userguide/dockervolumes/)  
- If you choose to map the exposed directories, the directories you will need to create elsewhere are /uploads, /uploads/thumb, /uploads/medium, /uploads/import, /uploads/big, and /data.  They should all have permissions set to 777.  

# Base Docker Image
[phusion/baseimage-docker](https://registry.hub.docker.com/u/phusion/baseimage/)

# Installation

## Install Docker.

Download automated build from public Docker Hub Registry: docker pull kdelfour/lychee-mysql-docker

(alternatively, you can build an image from Dockerfile: docker build -t="kdelfour/lychee-mysql-docker" github.com/neosar/lychee-docker)

## Usage

    docker run -it -d -p 80:80 kdelfour/lychee-mysql-docker

You can add a shared directory as a volume directory with the argument *-v /your-path/uploads/:/uploads/ -v /your-path/data/:/data/ -v /your-path/plugins/:/plugins/* like this :

    docker run -it -d -p 80:80 -v /your-path/uploads/:/uploads/ -v /your-path/data/:/data/ -v /your-path/plugins/:/plugins/ kdelfour/lychee-mysql-docker

A mysql server with a database is ready if you want to use the docker-compose file provided in the git repository, you can use it with this parameters :

    url : mysql
    database name : lychee
    user name : lychee
    user password : lychee

## Build and run with custom config directory

Get the latest version from github

    git clone https://github.com/kdelfour/lychee-mysql-docker
    cd lychee-mysql-docker/

Build it

    sudo docker build --force-rm=true --tag="$USER/lychee-mysql-docker:latest" .

And run

    sudo docker run -d -p 80:80 -v /your-path/uploads/:/uploads/ -v /your-path/data/:/data/ -v /your-path/plugins/:/plugins/ $USER/lychee-mysql-docker:latest

Enjoy !!
