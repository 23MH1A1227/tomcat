pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/23MH1A1227/tomcat.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop keerthi-app || true
                docker rm keerthi-app || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi keerthi || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t keerthi .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 8890:8080 --name keerthi-app keerthi'
            }
        }
    }
}
