## Investigate available mounts
Docker:  
Docker has three mount types: volumes, bind mounts, and tmpfs mounts.  
Volumes:  
This is a mount where the container manages it and it can also be shared with other containers.  
Bind mounts:  
This is where the host machines file systems are mounted to the container but the container doesn't control it, the host does.  
tmpfs mounts:  
This is a mount where as soon as a ontainer is stopped, the data that was in the mount will be lost with the container.  

Singularity:  
Fuse:  
This allows filesystems to run in a userspace after being mounted.  
Image:  
This allows you to mount an image file to a container. We can use this to take many folders/files and bring them into a single image file.  

## Investigate building images for the container engine