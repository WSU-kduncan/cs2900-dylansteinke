## Installing
These are the steps I took to install Docker:
```
1. sudo apt-get update
2. sudo apt-get install
3. sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
4. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
5. echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
6. sudo apt-get install docker-ce docker-ce-cli containerd.io
7. sudo apt install docker.io
```
These are the steps I took to install LXC:
```
1. sudo apt-get install lxc
```

## Pulling a container image
Docker:  
To pull image: sudo docker image pull alpine  
To view images: sudo docker images  
Lxc:  
To pull image: sudo lxc launch images:alpine/edge a2  
To view images: lxc image list  

## Running a container
There are different ways to run a container. One of these are detached mode and one is the shell. In detached mode, this is where the container runs in the backgrond. In shell mode, this is where it run like normal by running the typical commands.  
Containers can also be initalized or they can also be running. When initalizing a container, this is where we can specify the ammount of recourses that we want it to use. When we run the container, this is where the container is actually doing things.  
To run in shell mode for docker: sudo docker run alpine  
To run in detached mode for docker: sudo docker run -d alpine  
To run in shell mode for lxc: sudo lxc start a2  
To run in detached mode for lxc: lxc does not have a detached mode. Instead it itself is a lightweight Linux container, because of this, we can SSH into the container and make it act as an OS and then install an application. We can not do this with docker though because it acts as the "base os."

## Logs and Status
To find out the status of a container in docker: sudo docker ps  
To find the log of a specific container in docker: docker logs "container ID"  
To find out the status of a container in lxc: lxc info "name"  
To find the log of a specific container in lxc: We must first start one by using the command: lx-monitor -n "name"  
Once we do this, in the container we can do what we want and when we are done, go to the log file and see them there.

## Stopping a container
### Docker:
Pause: docker pause "container ID"  
Restart/resume: docker restart "container ID"  
Stop/kill: docker kill "container ID"  
To removed a stopped container: docker rm "container ID"

### LXC
Pause: lxc pause "name"  
Restart: lxc restart "name"  
Resume: lxc start "name"  
Stop/kill: lxc stop "name"  
To remove a stopped container: lxc delete "name"