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
                sh './jenkins/scripts/deploy.sh "dev" 2 3 4 5 "$DEV_ENVIRONMENT_CREDS_USR" "$DEV_ENVIRONMENT_CREDS_PSW" 8 9 10 11 12 13 14 15 16 17 18'
            }
        }
        stage('Staging deployment approval') {
            timeout(time:3, unit:'DAYS') {
                env.IS_APPROVED = input(
                id: "APPROVE_TO_STAGING",
                message: "Do you want to proceed to deploy in Staging?",
                ok: "OK",
                parameters:[booleanParam(defaultValue:false, name: 'Approve', description: 'Deploy to Staging?')])
                if (env.IS_APPROVED != 'true') {
                    echo "Approval to deploy in staging was Declined."
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh './jenkins/scripts/deploy.sh "staging" 2 3 4 5 "$DEV_ENVIRONMENT_CREDS_USR" "$DEV_ENVIRONMENT_CREDS_PSW" 8 9 10 11 12 13 14 15 16 17 18'
            }
        }
    }
}