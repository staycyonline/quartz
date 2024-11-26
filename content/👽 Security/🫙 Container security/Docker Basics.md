Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[]] - index location 

#### Summary
Basics of docker

#### Intro
- Dockerfile contains all the commands and base OS details
- Image - a unit where all Os, dependencies and config is defined
- Container - Instance of an image
- `docker build -t name:latest.`  - Builds image from dockerfile
- `docker images` - shows list of images
- `docker pull image_name` - pulls image from dockerhub
- `docker run -itd -p 8080:80 imagename:latest`  - start a container from image 
	- i - interactive
	- d - daemon mode
	- t - assign false tty
	- 8080 - port on host device
	- 80 - exposed port in image

- `docker ps` - lists the running containers
- `docker exec -it ContainerID command`
- `docker run -itd --name newname imagename` - create a container named new name from image imagename and execute
- `docker stop` - stops all docker containers
- `docker rmi` - removes all images from disk
- `docker rm` - removes all containers from disk
-  Note: We can use first 4 characters of container ID instead of the whole ID

----------------------------------

#### How docker container is stored on disk

- `docker info` - gives info about docker, profiles, storage location
- `docker inspect imagename` - gives info about a particular image
- Anyone with root access on host will have complete control over the containers and its contents
- Docker forms intermediate layers after each instruction
---

##### Control Groups

- It helps to limit access to resources availble for containers
- Crucial for avoiding forkbombs
- `find /sys/fs/cgroup/ -name "image name" ` to find cgroup entries
-  pid entrys are of great interest
- on navigating  to folder you can find pids.max - if it is max it is dangerous ❗
- `docker run -itd --pids-limit 6 imagename` - pids-limit sets the pid limit to 6 in this example
---
##### Namespaces

- Namspaces are used  to provide containers isolation from host
- Docker uses the following namspaces on linux
	- PID - for process isolation
	- NET - for managing network interfaces
	- IPC  - for managing IPC resource access
	- MNT - for managing filesystem mount points
	- UTS - for isolating kernel and version identifiers
	- User ID for privilage isolation
 - root on container can make changes in roots in host - usually without namespace



 #### References  (optional )
- https://infosecwriteups.com/beginners-guide-to-container-security-f7e671522ae3
- https://docs.docker.com/engine/security/
- https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html
- https://resources.infosecinstitute.com/topic/how-to-run-containers-securely/