
DockerFile 

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. 
The docker build command builds an image from a Dockerfile and a context.
docker build .
docker build -f /path/to/a/Dockerfile .
 docker build -t shykes/myapp .

The Docker daemon runs the instructions in the Dockerfile one-by-one, committing the result of each instruction to a new image if necessary, before finally outputting the ID of your new image.
Whenever possible, Docker uses a build-cache to accelerate the docker build process significantly.
When you’re done with your build, you’re ready to look into scanning your image with docker scan


Docker file format
  ```sh
   # Comment
   INSTRUCTION arguments
  ```

  A Dockerfile must begin with a FROM instruction. 

  Docker distributes official versions of the images that can be used for building Dockerfiles under docker/dockerfile repository on Docker Hub.


An ARG declared before a FROM is outside of a build stage, so it can’t be used in any instruction after a FROM

RUN has 2 forms:

RUN <command> (shell form, the command is run in a shell, which by default is /bin/sh -c on Linux or cmd /S /C on Windows)
RUN ["executable", "param1", "param2"] (exec form)
The RUN instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile.



The CMD instruction has three forms:

CMD ["executable","param1","param2"]  (exec form, this is the preferred form)
CMD ["param1","param2"]  (as default parameters to ENTRYPOINT)
CMD command param1 param2 (shell form)

Note: There can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take effect.
The main purpose of a CMD is to provide defaults for an executing container. 


Do not confuse RUN with CMD. RUN actually runs a command and commits the result; CMD does not execute anything at build time, but specifies the intended command for the image.

LABEL
The LABEL instruction adds metadata to an image. A LABEL is a key-value pair. T

`EXPOSE`
The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. 
To set up port redirection on the host system, see using the -P flag.
The docker network command supports creating networks for communication among containers without the need to expose or publish specific ports, because the containers connected to the network can communicate with each other over any port. 

`ENV` - The ENV instruction sets the environment variable <key> to the value <value>.

`ADD` - The ADD instruction copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.

If <src> is a local tar archive in a recognized compression format (identity, gzip, bzip2 or xz) then it is unpacked as a directory. 

`COPY` - The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.

`ENTRYPOINT` - An ENTRYPOINT allows you to configure a container that will run as an executable.

ENTRYPOINT will override all elements specified using CMD


Understand how CMD and ENTRYPOINT interact

Both CMD and ENTRYPOINT instructions define what command gets executed when running a container. There are few rules that describe their co-operation.

Dockerfile should specify at least one of CMD or ENTRYPOINT commands.

ENTRYPOINT should be defined when using the container as an executable.

CMD should be used as a way of defining default arguments for an ENTRYPOINT command or for executing an ad-hoc command in a container.

CMD will be overridden when running the container with alternative arguments.

VOLUME - The VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers. 

USER - The USER instruction sets the user name to use when running the image
WORKDIR - The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions

ARG - The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag. 

SHELL - The SHELL instruction allows the default shell used for the shell form of commands to be overridden. 


