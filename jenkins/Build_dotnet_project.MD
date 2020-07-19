# Build a .net project

## Pre-requisites
1. Jenkins server 
2. Windows server as Jenkins agent 

## Procedure
1. Setup Windows as a client on Jenkins server
2. Install MSbuild plugin on Master
3. Install MSbuild packages on windows agent server (From chocolatey.org)
4. Install Nuget, Nunit package on Windows agent server
5. Create a Jenkins Job
   GitHub URL: https://github.com/executeautomation/SeleniumNUnitParam