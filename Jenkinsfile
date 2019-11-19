pipeline {
    environment {
        DEV_ENVIRONMENT_CREDS = credentials('dev_env')
    }

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
        stage('Deploy to Dev') {
            steps {
                sh "echo $DEV_ENVIRONMENT_CREDS_USR"
                sh "echo $DEV_ENVIRONMENT_CREDS_PSW"
                sh './jenkins/scripts/deploy.sh "dev" 1 2 3 4 5 "$DEV_ENVIRONMENT_CREDS_USR" "$DEV_ENVIRONMENT_CREDS_PSW" 8 9 10 11 12 13 14 15 16 17 18'
            }
        }
    }
}