pipeline {
    agent none
//     environment {
//         BRANCH_NAME = "${env.GIT_BRANCH.replaceFirst(/^.*\//, '')}"
//         ENV_NAME = getEnvName(env.BRANCH_NAME)
//     }
    stages {
//         stage('Tests') {
//             agent any
//             steps {
//                 echo BRANCH_NAME
//                 echo ENV_NAME
//             }
//         }
        stage('Build') {
            agent {
                docker { image 'maven:3.6.0-jdk-8-slim'}
            }
            steps {
                sh 'mvn clean package -DskipTests -Pprod'
            }
        }
        stage('Test') {
            agent {
                docker { image 'maven:3.6.0-jdk-8-slim'}
            }
            steps {
                sh 'mvn -Pprod -B test'
            }
        }
//         stage('JaCoCo report') {
//             agent {
//                 docker { image 'maven:3.6.0-jdk-8-slim'}
//             }
//             steps {
//                 sh 'mvn -Pprod -B jacoco:report'
//             }
//         }
//         stage('Sonarqube') {
//             agent {
//                 docker { image 'maven:3.6.0-jdk-8-slim'}
//             }
//             steps {
//                 sh 'mvn -P${ENV_NAME} -B sonar:sonar'
//             }
//         }
//         stage('Down Build container') {
//             when {
//                 expression { ENV_NAME == 'dev' }
//             }
//             steps {
//                 sh 'docker-compose -f docker-compose.${ENV_NAME}.yml down'
//             }
//         }
    }
//     post {
//         always {
//             emailext to: "nonstopintegration@gmail.com",
//                      subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
//                      attachLog: true,
//                      body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
//         }
//     }
}

def getEnvName(branchName) {
    if (branchName.startsWith("release-")) {
        return 'prod';
    } else if (branchName == "preprod") {
        return 'preprod';
    }

    return "dev";
}