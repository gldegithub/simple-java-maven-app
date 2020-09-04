pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args ' -u root -v /home/jenkins/mvnrepo:/root/.m2'
        }
    }
    stages {
        stage('Pull Git Demo') {
            steps{
                //拉取代码
            	git 'https://github.com/gldegithub/simple-java-maven-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
