# Integrate Artifactory with Jenkins

## pre-requisites
1. An Artifactory server [Click here to create]()
1. A Jenkins Server [Click here to create]()

## Integration Steps
Login to Jenkins to integrate Artifactory with Jenkins  

1. Install "Artifactory" plug-in   
- `Manage Jenkins` -> `Jenkins Plugins` -> `available` -> `artifactory`

2. Configure Artifactory server credentials   
- ` Manage Jenkins` -> `Configure System` -> `Artifactory`
   - Artifactory Servers
      - Server ID : `Artifactory-Server`
      - URL : `Artifactory Server URL`
      - Username : `admin`
      - Password : `admin@123
    
---
---
### Create a Freestyle Project 
  
1. Create a new job 
  - Job Name : `artifactory-project`
  - Source code management 
     - Git URL : [get URL here](https://github.com/yankils/hello-world.git)
 - Build Environment 
     - Maven3-Artifactory Integration : `<provide Artifactory server and repository details
>`
 - Build --> Invoke Artifactory Maven3  
       - Goals: ` clean install`

2. Execute job 
---
---
### Create a Maven Project

1. Create a new job 
  - Job Name : `artifactory-project`
  - Source code management 
     - Git URL : [get URL here](https://github.com/yankils/hello-world.git)
 - Build Environment 
     - Resolve artifacts from Artifactory : `<provide Artifactory server and repository details>`
 - Build 
       - Goals: ` clean install`
 - Post-build Actions
   - Deploy Artifacts to Artifactory : `<provide Artifactory server and repository details>`

2. Execute job 