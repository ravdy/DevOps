# Setup Jfrog Artifactory 

## Pre-requisites: 
1. Setup an AWS T2.Small EC2 instance

## Installation Steps 

1. Install Java
   ```sh 
 	yum install java-1.8* -y 
   ```
1. Download Artifaction packages from 

   ```sh 
	wget https://bintray.com/jfrog/artifactory-pro/download_file?file_path=org%2Fartifactory%2Fpro%2Fjfrog-artifactory-pro%2F6.19.1%2Fjfrog-artifactory-pro-6.19.1.zip
   ```

1. extract artifactory zip file
   ```sh
     unzip download_file?file_path=org%2Fartifactory%2Fpro%2Fjfrog-artifactory-pro%2F6.19.1%2Fjfrog-artifactory-pro-6.19.1.zip 
   ```
1. start artifactory services 
   ```sh
      cd artifactory-pro-6.19.1/bin 
      ./artifactory.sh start
   ```
1. access artifactory from browser
   ```sh
     http://<IP_Address>:8081 
   ```

1. Provide credentials 
   ```sh 
      username: admin
      password: passwrod 
   ```
   