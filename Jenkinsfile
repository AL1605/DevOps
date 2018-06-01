pipeline{
    agent any
    environment{
        imageName = "al1605/al-nginx"
    }
    stages{
        stage("Build Images"){
            steps{
                sh "docker build -t ${env.imageName} ."
                sh "docker tag ${env.imageName} ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Push Images"){
            steps{
                script{
                    docker.withRegistry(
                        'https://registry.hub.docker.com', 'docker-id'
                        //'https:docker.io', 'docker-id'
                    ){
                        def customImage = docker.build("${env.imageName}:1.${env.BUILD_NUMBER}")
                        customImage.push()
                    }
                }
            }
        }
        stage("Remove Images"){
            steps{
                sh "docker rmi ${env.imageName}:1.${env.BUILD_NUMBER}"
                sh "docker rmi registry.hub.docker.com/${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Pull Images"){
            steps{
                sh "docker pull ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Create Container"){
            steps{
                sh "docker run -d -p 8888:80 ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
    }
}
