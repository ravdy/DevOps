pipeline {
    agent any

    environment {
        NAME = 'AR'
        LASTNAME = 'Shankar'
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo $NAME $LASTNAME'
            }
        }
    }
}