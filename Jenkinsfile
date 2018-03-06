pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v /Users/cshan/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Create Docker Image') {
            agent {
                node {
                    customWorkspace '/Users/cshan/.jenkins/workspace/eurekaserver-pipeline'
                }
            }
            steps {
                sh 'cp ./docker/Dockerfile /Users/cshan/devops/apps/eurekaserver'
                sh 'cp ./target/eurekaserver-1.0.0.jar /Users/cshan/devops/apps/eurekaserver'
                sh 'cd /Users/cshan/devops/apps/eurekaserver && docker build --rm -t eurekaserver:1.0 .'
            }
        }
        stage('Deploy') {
            agent {
                node {
                    customWorkspace '/Users/cshan/devops/apps/eurekaserver'
                }
            }
            steps {
                sh 'docker stop eurekaserver'
                sh 'docker container rm -f eurekaserver'
                sh 'docker run -tid -it -p 9099:9099 --name eurekaserver eurekaserver:1.0'
            }
        }
    }
}