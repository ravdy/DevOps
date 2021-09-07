
# Sonarqube Setup

SonarQube is an open-source static testing analysis software, it is used by developers to manage source code quality and consistency.
## 🧰 Prerequisites
1. Need an EC2 instance (min t2.small)
2. Install Java-11
  ```sh 
   apt-get update   
   apt-get list | grep openjdk-11  
   apt-get install openjdk-11-jdk -y   
   ```

## Install & Setup Postgres Database for SonarQube
`Source: https://www.postgresql.org/download/linux/ubuntu/`  
1. Install Postgres database   
  ```sh 
  sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'  
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
  sudo apt-get update
  sudo apt-get -y install postgresql
  ```

1. Set a password and connect to database (setting password as "admin" password)
  ```sh 
  sudo passwd postgres
  su - postgres
  ```

1. Create a database user and database for sonarque 
  ```sh 
  createuser sonar
  psql
  ALTER USER sonar WITH ENCRYPTED PASSWORD 'admin';
  CREATE DATABASE sonarqube OWNER sonar;
  GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;
  ``` 

1. Restart postgres database to take latest changes effect 
  ```sh 
  systemctl restart postgresql 
  systemctl status postgresql
  ```
`check point`: You should see postgres is running on 5432



apt install net-tools

`Source: https://docs.sonarqube.org/latest/requirements/requirements/`

1. Added below entries in `/etc/sysctl.conf`
  ```sh 
  vm.max_map_count=524288
  fs.file-max=131072
  ulimit -n 131072
  ulimit -u 8192
  ```
1. Add below entries in `/etc/security/limits.conf`
  ```sh 
  sonarqube   -   nofile   131072
  sonarqube   -   nproc    8192
  ```

1. reboot the server 
  ```sh 
  init 6
  ```
  ==========================================

 ## SonarQube Setup

1. Download [soarnqube](https://www.sonarqube.org/downloads/) and extract it.   
  ```sh 
  wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.2.46101.zip
  unzip sonarqube-8.9.2.46101.zip
  ```

1. Update sonar.properties with below information 
  ```sh
  sonar.jdbc.username=<sonar_database_username>
  sonar.jdbc.password=<sonar_database_password>

  #sonar.jdbc.username=sonar
  #sonar.jdbc.password=admin
  #sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
  #sonar.search.javaOpts=-Xmx512m -Xms512m -XX:MaxDirectMemorySize=256m -XX:+HeapDumpOnOutOfMemoryError
  ``

1. Create a `/etc/systemd/system/sonarqube.service` file start sonarqube service at the boot time 
  ```sh   
  cat >> /etc/systemd/system/sonarqube.service <<EOL
  [Unit]
  Description=SonarQube service
  After=syslog.target network.target

  [Service]
  Type=forking
  User=sonar
  Group=sonar
  PermissionsStartOnly=true
  ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start 
  ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
  StandardOutput=syslog
  LimitNOFILE=65536
  LimitNPROC=4096
  TimeoutStartSec=5
  Restart=always

  [Install]
  WantedBy=multi-user.target
  EOL
  ```

1. Add sonar user and grant ownership to /opt/sonarqube directory 
  ```sh 
  useradd -d /opt/sonarqube sonar
  chown -R sonar:sonar
  ```

1. Reload the demon and start sonarqube service 
  ```sh 
  systemctl daemon-reload 
  systemctl start sonarqube.service 
  ```


## 🧹 CleanUp  

   Stop sonarqube services and delete the instance

 ## Unable to access Sonarqube from browser? 

 1. Make sure port 9000 is opened at security group leave
 2. start sonar service as a sonar user 
 3. user correct database credentials in the sonar.properties
 4. user instance which has atleast 2 GB of RAM
 

   
## 🔗 My Profile
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://www.udemy.com/user/ar-shankar/)  
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ravdsun/)


  ### 💡 Help/Suggestions or 🐛 Bugs

Thank you for your interest in contributing to our project. Whether it is a bug report, new feature, correction, or additional documentation or solutions, we greatly value feedback and contributions from our community. [Start here](/issues)   
