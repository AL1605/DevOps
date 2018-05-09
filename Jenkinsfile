pipeline{
    agent any
    stages{
        stage("Prepare"){
            steps{
                echo "AL Nunim"
            }
        }
        stage("Check Version"){
            steps{
                sh "docker --version"
            }
        }
        stage("Build Images"){
            steps{
                sh "docker build -t al-nginx ."
                sh "docker tag al-nginx:1.${env.BUILD_NUMBER} al-nginx"
            }
        }
    }
}