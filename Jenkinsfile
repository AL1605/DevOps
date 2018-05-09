pipeline{
    agent any
    environment{
        /*imageName = "al-nginx"*/
        imageName = "al1605/al-nginx"
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
                sh "docker tag ${env.imageName} ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Push Images"){
            steps{
                /*sh "docker login -u xxxx -p xxxx"*/
                sh "docker push ${env.imageName}"
            }
        }
    }
}