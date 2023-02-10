# Dockerfile
Dockerfile is a text document that contains set of commands and instructions which will be executed in a sequence in the docker environment for building a new docker image.

# FROM
This command Sets the Base Image for subsequent instructions

FROM <image>
FROM <image>:<tag>
FROM <image>@<digest>

Example:
FROM ubuntu:18.04

# RUN
RUN instruction allows you to install your application and packages required for it. It executes any commands on top of the current image and creates a new layer by committing the results. It is quite common to have multiple RUN instructions in a Dockerfile.

It has two forms

  Shell Form: RUN
  RUN npm start

  Exec form RUN ["", "", ""]
  RUN [ "npm", "start" ]

# ENTRYPOINT
An ENTRYPOINT allows you to configure a container that will run as an executable. It is used to run when container starts.

  Exec Form:
  ENTRYPOINT ["executable", "param1", "param2"]

  Shell Form:
  ENTRYPOINT command param1 param2

  Example:
  FROM alpine:3.5
  ENTRYPOINT ["/bin/echo", "Print ENTRYPOINT instruction of Exec Form"]
  If an image has an ENTRYPOINT and pass an argument to it while running the container, it wont override the existing entrypoint but it just appends what you passed with the entrypoint. To override the existing ENTRYPOINT. you should user –entrypoint flag for the running container.

  Let's see the behavior with the above dockerfile,

  Build image:
  docker build -t entrypointImage .

  Run the image:
  docker container run entrypointImage // Print ENTRYPOINT instruction of Exec Form

  Override entrypoint:
  docker run --entrypoint "/bin/echo" entrypointImage "Override ENTRYPOINT instruction" // Override ENTRYPOINT instruction

# CMD
CMD instruction is used to set a default command, which will be executed only when you run a container without specifying a command. But if the docker container runs with a command, the default command will be ignored.

The CMD instruction has three forms,

  1. Exec form:
  CMD ["executable","param1","param2"]

  2. Default params to ENTRYPOINT:
  CMD ["param1","param2"]

  3. Shell form:
  CMD command param1 param2

  The main purpose of the CMD command is to launch the required software in a container. For example, running an executable .exe file or a Bash terminal as soon as the container starts.

  Remember, if docker runs with executable and parameters then CMD instruction will be overridden(Unlike ENTRYPOINT).

  docker run executable parameters
  Note: There should only be one CMD command in your Dockerfile. Otherwise only the last instance of CMD will be executed.

# COPY
The COPY instruction copies new files or directories from source and adds them to the destination filesystem of the container.

  COPY [--chown=<user>:<group>] <src>... <dest>
  COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]

  Example:
  COPY test.txt /absoluteDir/
  COPY tes? /absoluteDir/ // Copies all files or directories starting with test to destination container
  The path must be relative to the source directory that is being built. Whereas is an absolute path, or a path relative to WORKDIR.

# ADD
The ADD instruction copies new files, directories or remote file URLs from source and adds them to the filesystem of the image at the destination path. The functionality is similar to COPY command and supports two forms of usage,

  ADD [--chown=<user>:<group>] <src>... <dest>
  ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]

  Example:
  ADD test.txt /absoluteDir/
  ADD tes? /absoluteDir/ // Copies all files or directories starting with test to destination container
  ADD commands provides additional features such as downloading remote resources, extracting TAR files etc.

  1. Download an external file and copy to the destination
  ADD http://source.file/url  /destination/path

  2. Copies compressed files and extract the content in the destination
  ADD source.file.tar.gz /temp

# ENV
The ENV instruction sets the environment variable to the value . It has two forms,

The first form, ENV <key> <value>, will set a single variable to a value.
The second form, ENV <key>=<value> ..., allows for multiple variables to be set at one time.
ENV <key> <value>
ENV <key>=<value> [<key>=<value> ...]

Example:
ENV name="John Doe" age=40
ENV name John Doe
ENV age 40

# EXPOSE
The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. i.e, It helps in inter-container communication. You can specify whether the port listens on TCP or UDP, and the default is TCP.

  EXPOSE <port> [<port>/<protocol>...]

  Example:
  EXPOSE 80/udp
  EXPOSE 80/tcp
  But if you want to bind the port of the container with the host machine on which the container is running, use -p option of docker run command.

  docker run -p <HOST_PORT>:<CONTAINER:PORT> IMAGE_NAME

  Example:
  docker run -p 80:80/udp myDocker

# WORKDIR
The WORKDIR command is used to define the working directory of a Docker container at any given time for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.

  WORKDIR /path/to/workdir

  Example:
  WORKDIR /c
  WORKDIR d
  WORKDIR e
  RUN pwd  // /c/d/e

# LABEL
The LABEL instruction adds metadata as key-value pairs to an image. Labels included in base or parent images (images in the FROM line) are inherited by your image.

  LABEL <key>=<value> <key>=<value> <key>=<value> ...

  Example:
  LABEL version="1.0"
  LABEL multi.label1="value1" \
        multi.label2="value2" \
        other="value3"
  You can view an image’s labels using the docker image inspect --format='' myimage command. The output would be as below,

  {
    "version": "1.0",
    "multi.label1": "value1",
    "multi.label2": "value2",
    "other": "value3"
  }

# MAINTAINER
The MAINTAINER instruction sets the Author field of the generated images.

MAINTAINER <name>

Example:
MAINTAINER John
This command is deprecated status now and the recommended usage is with LABEL command

LABEL maintainer="John"

# VOLUME
The VOLUME instruction creates a mount point with the specified name and mounted volumes from native host or other containers.

VOLUME ["/data"]

Example:
FROM ubuntu
RUN mkdir /test
VOLUME /test