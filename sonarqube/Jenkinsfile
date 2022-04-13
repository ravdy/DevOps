pipeline{
    agent any
    environment {
        PATH = "$PATH: C:/Program Files/maven/apache-maven-3.8.5/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/Mifathim28/test1.git'
                
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-9.4') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
       
    }
}
