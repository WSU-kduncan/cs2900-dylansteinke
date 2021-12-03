# Investigate Container Networking  
## Docker:  

1. Networking modes and their capabilities:  
    There are three networking modes for docker.  
        - Host: Which shared the network stack with the host machine which means there is no namespace isonlation.  
        - None: Which is where the container is fully isolated namespace and there are no routes.  
        - Bridge: This is where the namespace is not shared with the host machine. It routes trafic to the host and can then be port forwarded.  
2. What networking mode is used by default:  
    The default netowrking mode is bridge.  
3. How to run the container and bind a host port to the container port:  
    This is the command used:  
    ```
    docker run -dit -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
    ```


## Singularity:  
1. Networking modes and their capabilities:  
    There are four networking types for singularity:  
        - Bridge: This is where the name space is different from the host and it routes traffice to the host and can be port forwarded.  
        - Ptp: This creates a point-to-point link between the host and the container via a device. The traffic of the container will go through the host. Source Used: [cni.dev](https://www.cni.dev/plugins/current/main/ptp/)  
        - IPvlan: This does not allow the container to communicate with the host. Source Used: [cni.dev](https://www.cni.dev/plugins/current/main/ipvlan/)  
        - Macvlan: This is where the host and container are connected together, but they wach get a unique IP Address. Source Used: [cni.dev](https://www.cni.dev/plugins/current/main/macvlan/)  
2. What networking mode is used by default:  
    The default netowking mode is bridge. Source Used: [sylabs.io](https://sylabs.io/guides/3.0/user-guide/networking.html)  
3. How to run the container and bind a host port to the container port:  
    This is the command used:  
    ```
    sudo singularity instance start --writable-tmfs \  
    -- net -network-args "portmap=OUTSIDE_PORT:INSIDE_PORT/tcp" docker://nginx web2
    ```
    Source Used: [sylabs.io](https://sylabs.io/guides/3.0/user-guide/networking.html)  

# Investigate Vulnerability Scanners
1. Find a Dockerfile linter. What best practices does it look for?  
    Hadolint is a Dockerfile linter for VSCode. This will look for spaces after = when trying to assign a value, will delete the apt-get list after being ran, and check if node_version is ever referenced but not assigned. Source Used: [github.com](https://github.com/hadolint/hadolint)  
2. Find a scanner that can scan images for vulnerabilities.  
    I will be using Aqua Trivy.  
        Does it have any limits on what can be scanned?  
            - Source Used for the following: [docs.securecodebox.io](https://docs.securecodebox.io/docs/scanners/trivy/)  
            - It can only scan container images when scanning Many Targets at a time.  
            - When wanting to scan something other than a docker file, it requires extra parameters.  
        What types of vulnerabilities are scanned?  
            - It will scan OS packages and language-specific packages. With this it will search for glitches, flaws, and weaknesses.  
            - The other thing that it can scan is IaC files. With this it will detect potential configuration issues that would expose deployments to risks. There is no other things that are specified that it can scan. Source Used: [aquasecurity.github.io](https://aquasecurity.github.io/trivy/v0.21.0/)