pipeline{

    agent any

    stages{

        stage('Build Jar'){
            steps{
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Image'){
            steps{
                sh 'docker build -t=deepinder9399/selenium:latest .'
            }
        }

        stage('Push Image'){
            environment{
                DOCKER_HUB = credentials('mydocker-hubcredentials')
            }
            steps{
                sh 'echo ${DOCKER_HUB_PSW} | docker login -u ${DOCKER_HUB_USR} --password-stdin'
                sh 'docker push deepinder9399/selenium:latest'
                sh "docker tag deepinder9399/selenium:latest deepinder9399/selenium:${env.BUILD_NUMBER}"
                sh "docker push deepinder9399/selenium:${env.BUILD_NUMBER}"
            }
        }

    }

    post {
        always {
            sh 'docker logout'
        }
    }

}
