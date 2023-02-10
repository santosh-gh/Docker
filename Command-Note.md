# Docker Registry and Repository
    - Login to a Registry
        docker login
        docker login localhost:8080

    - Logout from a registry:
        docker logout
        docker logout localhost:8080

    - Searching an image (search nginx)
        docker search --filter stars=3 --no-trunc nginx

    - Pulling an Image
        docker image pull nginx
        docker image pull eon01/nginx localhost:5000/myadmin/nginx
    
    - Pushing an image
        docker image push eon01/nginx
        docker image push eon01/nginx localhost:5000/myadmin/nginx

# Running Containers
    - Command to create a container
        docker container create -t -i eon01/infinite --name XYZ

    - Command to run a container
        docker container run -it --name XYZ -d eon01/infinite

    - Command to rename a container
        docker container rename XYZ infinity
    
    - Command for removing a container
        docker container rm infinite

    - Update a container
        docker container update --cpu-shares 512 -m 300M infinite

# Starting / Stoping Containers
    - Command for starting a container		
        docker container start nginx

    - Command for stopping a container	
        docker container stop nginx

    - Command for restarting the container	
        docker container restart nginx

    - Command for pausing the container	
        docker container pause nginx

    - Command for unpausing the container		
        docker container unpause nginx

    - Command for Blocking a container		
        docker container wait nginx

    - Sending a SIGKILL		
        docker container kill nginx

    - Command for sending another signal		
        docker container kill -s HUP nginx

    - Command for Connecting to an Existing Container	
        docker container attach nginx

# Commands for Obtaining Container Information
    - Fetching information From Running Containers	
        docker ps
        docker container ls

    - Command for fetching about every container	
        docker container ls -a
        docker ps -a

    - Command for container log		
        docker logs infinite

    - Command for ‘tail -f’ Containers’ Logs	
        docker container logs infinite -f

    - Command for Inspecting Containers	
        docker container inspect infinite
        docker container inspect --format '' $(docker ps -q)

    - Command for Containers Events	
        docker system events infinite

    - Command for Public Ports	
        docker container port infinite

    - Command for Running Processes		
        docker container top infinite

    - Command for Container Resource Usage		
        docker container stats infinite

    - Commands for Inspecting changes to files or directories on a container’s filesystem		
        docker container diff infinite

# Commands for Managing Images
    Commands for listing images	
    docker image ls

    Command for Building images From the current directory's Dockerfile	
    docker build 

    Command for Building images From a GIT remote repository	
    docker build github.com/creack/docker-firefox

    Commands for tagging and building	
    docker build -t eon/infinite 

    Specifying the Build Context while creating a Dockerfile	
    docker build -f myDockerfile

    Creating a Dockerfile from a URL	
    curl example.com/remote/Dockerfile | docker build -f - 

    Command for removing image	
    docker image rm nginx

    Using a File or the Normal Input Stream to Load a Tarred Repository	
    docker image load < ubuntu.tar.gz

    docker build -f myOtherDockerfile 

    Image Saving to a Tar Archiveard Input Stream	
    docker image save busybox > ubuntu.tar

    Showing the History of an Image	
    image history

    Making an Image Out of a Container	
    docker container commit nginx

    Command for image tagging	
    docker image tag nginx eon01/nginx

    Command for pushing an image	
    docker image push eon01/nginx

# Commands for Networking
    Command for overlay network	This is used to establish a distributed network between many Docker daemon hosts.	
    docker network create -d overlay MyOverlayNetwork

    Command for Bridge network	To establish container test1 to bridge demo-bridge, type docker network connect demo-bridge test1.	
    docker network create -d bridge MyBridgeNetwork

    Command for removing a network	This command s used to remove an overlay network 	
    docker network rm MyOverlayNetwork

    Command for network listing	This command is used to listing the overlay networks	
    docker network ls

    Command for Getting Information About a Network	We can get information about an overlay network with the help of this command	
    docker network inspect MyOverlayNetwork

    Command for Connecting a Running Container to a Network	By using this command we can connect a container to network	
    docker network connect MyOverlayNetwork nginx

    Command for Connecting a Container to a Network When it Starts	When the container starts we can use this command to connect a container to network	
    docker container run -it -d --network=MyOverlayNetwork nginx

    Command for Disconnecting a Container from a Network	We can use this Command for disconnecting a container from network	
    docker network disconnect MyOverlayNetwork nginx

    Command for Exposing Ports	We can expose the empty ports using this command	
    EXPOSE <port_number>

# Commands for Cleaning Docker
    Command for Removing a Running Container	We can remove a running container by using this command	
    docker container rm nginx

    Command for Removing a Container and its Volume	We  can use this command for removing the container and the things inside it	
    docker container rm -v nginx

    Command for Removing all Exited Containers	We can use this command for removing all the exited containers	
    docker container rm $(docker container ls -a -f status=exited -q)

    Command for Removing All Stopped Containers	We can remove all the stopped containers by using this command	
    docker container rm `docker container ls -a -q`

    Command for Removing a Docker Image	This command is used fr removing a docker image 	
    docker image rm nginx

    Command for Dangling Images	We can dangle the images with this command	
    docker image rm $(docker image ls -f dangling=true -q)

    Command for Removing all Images	We can remove all the image in the docker by using this commands	
    docker image rm $(docker image ls -a -q)

    Commands for Delete all Untagged Images	We can delete all the untagged images with the use of this command	
    docker image rm -f $(docker image ls | grep "^<none>" | awk "{print $3}")

    Command for Stopping & Removing all Containers	For stopping and removing all the container we can use this command	
    docker container stop $(docker container ls -a -q) && docker container rm $(docker container ls -a -q)

    Command for Removing Dangling Volumes	We can remove all the dangling volumes by using this command	
    docker volume rm $(docker volume ls -f dangling=true -q)

    Command for removing all unneeded (containers, images, networks and volumes)	This command is use to remove the unnecessary thing 	
    docker system prune -f

    Command for Clean all	We cam use this command for cleaning everything in the docker	
    docker system prune -a

# Running Containers
    docker run -it ubuntu bash	Run container and specify command
    docker run -it ubuntu	Run container
    docker run -tid ubuntu	Run container detatched
    docker create -ti ubuntu	Create a container without starting it
    docker run -tid --name smelly-hippo ubuntu	named container
    docker ps	show running containers
    docker ps -a	show all containers
    docker ps --filter name=web1	show matching containers
    docker ps --filter name=web1 -q	show matching container ID
    docker inspect smelly-hippo	inspect container

# Container Lifecycle Stuff
    docker start smelly-hippo	start
    docker stop smelly-hippo	stop
    docker stop smelly-hippo funny-frog	stop mutliple
    docker restart smelly-hippo	restart container
    docker pause smelly-hippo	pauses a running container, freeze in place
    docker unpause smelly-hippo	unpause a container
    docker wait smelly-hippo	blocks until running container stops
    docker kill smelly-hippo	sends SIGKILL, faster than stop
    docker rm smelly-hippo	remove
    docker rm smelly-hippo funny-frog	remove multiple
    docker rm -f smelly-hippo	force remove
    docker container rm -f $(docker ps -aq)	Remove all containers, running or stopped

# Resource Limits and Controls
    docker run -tid -c 512 ubuntu	50% cpu
    docker run -tid --cpuset-cpus=0,4,6 ubuntu	use these cpus
    docker run -tid -m 300M ubuntu	limit memory
    docker create -ti --storage-opt size=120G ubuntu	limit storage, not on aufs

# Stats, Logs, and Events
    docker stats	resourse stats for all containers
    docker stats smelly-hippo	resource stats for one container
    docker top smelly-hippo	shows processes in a container
    docker logs web	container logs
    docker events	watch events in real time
    docker port nostalgic_colden	shows public facing port of container
    docker diff practical_sinoussi	show changes to a container's file system

# Docker Images
    docker images	show images
    docker history ubuntu	show history of image
    docker image rm user1/funny-frog	remove image
    docker image remove 113a43faa138	remove by id
    docker image remove user1/funny-frog	remove image
    docker rmi user1/funny-frog	remove image
    docker rmi $(docker images -q)	remove all images
    Commit container to an image:
    docker commit smelly-hippo	no repo name
    docker commit smelly-hippo test1	repo name
    docker commit smelly-hippo loworbitflux/test1	repo name
    docker commit smelly-hippo loworbitflux/test1:my-update	tagged
    docker commit smelly-hippo loworbitflux/test1:v1.2.3	tagged

# Export / Import / Save / Load
    docker export	export container to tarball archive stream
    docker import	create image from tarball, excludes history ( smaller image )
    docker load	load an image from tarball, includes history ( larger image )
    docker save	save image to tar archive stream ( includes parent layers )

    Examples:
    docker load < my-image.tar.gz
    docker save my_image:my_tag | gzip > my-image.tar.gz
    cat my-container.tar.gz | docker import - my-image:my_tag
    docker export my-container | gzip > my-container.tar.gz

# Docker Hub / Registry
    docker login	Login to Registry
    docker logout	Logout of Registry
    docker tag 7d9495d03763 loworbitflux/smelly-hippo:latest	Tag an image
    docker push loworbitflux/smelly-hippo	Push to registry
    docker search mysql	Search for an image
    docker pull mysql	Pull it down
    docker run user1/funny-frog	Will be downloaded if it isn’t here

# Building Docker Images From A Dockerfile
    mkdir mydockerbuild	Create build dir
    cd mydockerbuild	cd into build dir
    vi Dockerfile	Edit build instructions
    docker build -t mydockerimage .	Build the image (note the dot "." )
    docker images	Show images
    docker run mydockerimage	Run the new image

# Simple Dockerfile Example
    FROM ubuntu
    RUN apt update
    RUN apt install nginx -y
    CMD ["/usr/sbin/nginx"]

# Big Dockerfile Example
    FROM ubuntu	base image
    RUN apt update	run commands while building
    RUN apt install nginx -y	run commands while building
    WORKDIR ~/	working dir that CMD is run from
    ENTRYPOINT echo	default application
    CMD "echo" "Hello docker!"	main command / default application
    CMD ["--port 27017"]	params for ENTRYPOINT
    CMD "Hello docker!"	params for ENTRYPOINT
    ENV SERVER_WORKS 4	set env variable
    EXPOSE 8080	expose a port, not published to the host
    MAINTAINER authors_name	deprecated
    LABEL version="1.0"	add metadata
    LABEL author="User One"	add metadata
    USER 751	UID (or username) to run as
    VOLUME ["/my_files"]	sets up a volume
    COPY test relativeDir/	copies "test" to `WORKDIR`/relativeDir/
    COPY test /absoluteDir/	copies "test" to /absoluteDir/
    COPY ssh_config /etc/ssh/ssh_config	copy over a vile
    COPY --chown=user1:group1 files* /data/	also changes ownership
    ADD /dir1 /dir2	like copy but does more ...

# Volumes / Storage
    docker info | grep -i storage	check storage driver
    docker inspect web	look for “Mounts”
    docker volume ls	show voluems
    docker volume create testvol1	create a volume
    docker volume inspect testvol1	inspect a volume
    docker volume ls -f dangling=true	find dangling ( unused ) volumes
    docker volume rm volume1	remove volume
    Running containers with volumes:
    docker run -d --name test1 -v /data ubuntu	unamed volume mounted on /data
    docker run -d --name test2 -v vol1:/data ubuntu	named volume
    docker run -d --name test3 -v /src/data:/data ubuntu	bind mount
    docker run -d --name test4 -v /src/data:/data:ro ubuntu	RO
    docker run -d --volumes-from test2 --name test5 ubuntu	storage can be shared
    docker rm -v test1	remove container and unnamed volume
    Access and sharing parameters:
    :ro	for read only
    :z	shared all containers can read/write
    :Z	private, unshared
    -
    /var/lib/docker/overlay2	Defalt volume storage location on Ubuntu Linux

# Expose Ports
    docker run -tid -p 1234:80 nginx	expose container port 80 on host port 1234
    docker run -tid -p 80:5000 ubuntu	bind port
    docker run -tid -p 8000-9000:5000 ubuntu	bind port to range
    docker run -tid -p 80:5000/udp ubuntu	udp ports
    docker run -tid -p 127.0.0.1:80:5000 ubuntu	bind port on an interface
    docker run -tid -p 127.0.0.1::5000 ubuntu	bind any port, specific interface
    docker run -tid -P ubuntu	exposed ports to random ports

# Networks
    docker network ls	show networks, bridge is default
    docker network inspect bridge	show network details and connected containers
    Create Bridge Network, Specify Subnet and Gateway:
    docker network create -d bridge my-network
    docker network create -d bridge --subnet 172.25.0.0/16 my-network
    docker network create --subnet 203.0.113.0/24 --gateway 203.0.113.254 my-network
    docker network rm my-network	remove network
    Run container and specify network:
    docker run -tid --net=my-network --name test1 ubuntu
    Run container, specify network and IP:
    docker run -tid --net=my-network --ip=172.25.3.3 --name=test1 ubuntu
    Connect container to network:
    docker network connect net1 test1
    docker network connect net1 test2 --ip 172.25.0.102
    Disconnect container from network:
    docker network disconnect net1 test1	Disconnect container from this network
    docker network disconnect -f test1 test2	Force disconnect
    Find container's IP address:
    docker inspect -f '{{json .NetworkSettings.Networks}}' container1
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container1

