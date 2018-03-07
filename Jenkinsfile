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
                    label 'master'
                }
            }
            steps {
                sh 'chmod 755 ./buildDockerImage && ./buildDockerImage'
            }
        }
        stage('Deploy') {
            agent {
                node {
                    label 'master'
                }
            }
            steps {
                sh 'chmod 755 ./deploy && ./deploy'
            }
        }
    }
}