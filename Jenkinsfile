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
                sh './jenkins/scripts/deploy.sh dev 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18'
            }
        }
    }
}