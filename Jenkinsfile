pipeline {
    agent any
    tools {
        maven 'apache-maven-3.6.2' 
    }

    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            // post {
            //     always {
            //         junit 'target/surefire-reports/*.xml'
            //     }
            // }
        }
        stage('Deliver') {
            steps {
                sh 'mvn clean install'
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}