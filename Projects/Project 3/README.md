# Investigate available mounts
## Docker:  
Docker has three mount types: volumes, bind mounts, and tmpfs mounts.  
Volumes:  
This is a mount where the container manages it and it can also be shared with other containers.  
To create a volume: ```sudo docker volume create NAME```  
To start a container with a volume:  
```
docker run -d \
--name devtest \
--mount source=NAME,target=/app \
nginx:latest
```  
Then we inspect using: ```docker inspect container_name```  
Source Used: [docs.docker](https://docs.docker.com/storage/volumes/)  
Bind mounts:  
This is where the host machines file systems are mounted to the container but the container doesn't control it, the host does.  
We would create a folder on the host then to run we would do the following:  
```
docker run -d \
-it \
--name devtest \
--mount type=bind,source=/file/path/folder,target=/container/folder \
busybox
```  
Then we inspect using: ```docker inspect container_name```  
tmpfs mounts:  
This is a mount where as soon as a ontainer is stopped, the data that was in the mount will be lost with the container.  

## Singularity:  
Singularity has two mount types: fuse and image mounts.  
Fuse:  
This allows filesystems to run in a userspace after being mounted.  
To use this we use the command: 
```--fusemount <type>:<fuse command> <container mountpoint>```  
Image:  
This allows you to mount an image file to a container. We can use this to take many folders/files and bring them into a single image file.  
To use this we use the command: ```-B <image-file>:<dest>:image-src=<source>```  
Source Used: [Sylabs](https://sylabs.io/guides/3.7/user-guide/bind_paths_and_mounts.html)


# Investigate building images for the container engine
## Docker:  
Yes, there are build tools available.  
The command to build an image is: ```docker build (options wanted) PATH/URL```  
For example if we want to build an image from gitub: ```docker build https://github.com/image/to/build/path.git#container:docker```  
How to write a build file:  
There are many things that we will/may need to create a build file. Some of these include FROM, WORKDIR, COPY, and RUN.  
```
FROM: This is used to add a base image to a dockerfile and the base image name goes after it  
WORKDIR: This is used to specifiy a directory that we can then copy files to  
COPY: This is used to copy files to the working directory from the source to the desination  
RUN: This is used to run a command such as installing something, updating the system, or running the package  
Extra... EXPOSE: this is used to "expose" a port. This is used to document what ports are being used.  
```

## Singularity:  
Yes, there are build tools available.  
The command to build an image is: ```sudo singularity build FILE docker:LOCATION```  
For example if we want to use one called lolcow.sif: ```sudo singularity build lolcow.sif docker://godlovedc/lolcow```  
Source Used: [Sylabs](https://sylabs.io/guides/3.0/user-guide/build_a_container.html)  
We can create a build file using many things. Such as:
```
Bootstrap: This allows us to 'break' compatibilty with older versions of software
From: This can be used if using a library bootstrap. This can specify for example which debian we would want to use.
%setup: This will be ran on the host system and not in the container. This can be used to create files, edit them, and more.
%files: This allows you to copy files into the container without the dangers of the host doing so with %setup.
%post: This is where we can get downloadable files from tools on the internet like git.
%test: This is where we can test the build at the end and verify the container.

NOTE: % items are all not required for a build file in singularity
```