# Build a docker image using Jenkins


### Pre-requisites

1. Jenkins server [Get help here]()
1. DockerHub account  

### Install docker and start docker on Jenkins server 
```sh 
  yum install docker -y
```
### On Jenkins Console 

Install "docker", "docker-build-step" and "CloudBees Docker Build and Publish" plugins 
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `docker`
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `docker-build-step`
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `CloudBees Docker Build and Publish`

Create dockerHub Credentials to store docker images

- `Credentials` > `System` > `Global Credentials` > `Add Credentials`
    - username: `valaxy`
    - Passwrod: `<password>`
    - ID: `dockerhub_user` 
               
 
### Steps to create "create_docker_image" Jenkin job
 #### From Jenkins home page select "New Item"
   - Enter an item name: `create_docker_image`
     
   - *Source Code Management:*
      - Repository: `https://github.com/yankils/hello-world.git`

   - *Build:*
          - Goals and options: `clean install`

   - *Docker build and publish*
          - Repository Name: `valaxy/hello_world
          - Registry credentials: `credentials`	

Save and run the job now.