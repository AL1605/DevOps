pipeline{
    agent any
    environment{
        imageName = "al-nginx"
    }
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
                sh "docker build -t ${env.imageName} ."
                sh "docker tag ${env.imageName}:1.${env.BUILD_NUMBER} ${env.imageName}"
            }
        }
    }
}