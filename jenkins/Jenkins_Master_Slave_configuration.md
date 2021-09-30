# Jenkins master and Slave configuration

## 🧰 Prerequisites
1. Jenkins Server 
2. Jenkins Agent server 

## Procedure: 
1. Goto Manage Nodes   
   - Manage Jenkins --> Manage Nodes and Clouds --> New Node  

2. Add the node name as Permanent Agent  
   
3. Provide below information to add Jenkins agent  
   **Name:** uniquely identifies an agent within this Jenkins installation  
   **Description:** <Description>  
   **Number of executors:** 2  
   **Remote root directory:** /home/ec2-user/maven-agent   
   **Labels:** Labels (or tags) are used to group multiple agents into one logical group.  
   **Usage:**  
   - Use this node as much as possible  
   - Only build jobs with label expressions matching this node   
 
   **Launch method:**   
   	  - Launch agent by connecting it to the master   
   	  - Launch agent via execution of command on the controller  

   **Custom WorkDir path:**  custom Remoting work directory will be used instead of the Agent Root Directory  
   **- Use WebSocket [x]**  
   **Availability:**  
   	- Keep this agent online as much as possible  
   	- Bring this agent online according to a schedule  
   	- Bring this agent online when in demand, and take offline when idle  

4. Once you save above configuration you will get a command which should be executed in the agent. it contains agent.jar, a secret-file, and a jnlp file 
   ```sh
     echo "secret_key" > secret-file
     java -jar agent.jar -jnlpUrl http://<Jenkins_URL>/computer/abc/jenkins-agent.jnlp -secret @secret-file -workDir "/home/ec2-user"
   ```
5. Once connected you can create or edit a job to chose this option in the `Restrict where this project can be run`


## Lessons Learned:   
  1. Master and slave should have  
     - same Java version  
     - Same Maven version   
  1. In case Jave or Maven paths are referring to the agent system then aline it according to masters `Global Tool Configuration`  
  1. In case the case of the AWS server make sure your Jenkins URL should be updated to the latest Public IP.   
  

## Contributing
Contributions are always welcome!

## 🧹 CleanUp 
  Is it a test environment? 
  stop or terminate Jenkins system 
  stop or terminate agent system 
  
## 🔗 My Profile
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://www.udemy.com/user/ar-shankar/)  
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ravdsun/)
