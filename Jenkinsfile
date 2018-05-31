pipeline{
    agent any
    environment{
        //imageName = "al-nginx"
        imageName = "al1605/al-nginx"
        containerName = "al-nginx"
    }
    stages{
        /*stage("Prepare"){
            steps{
                echo "AL Nunim"
            }
        }
        stage("Check Version"){
            steps{
                sh "docker --version"
            }
        }*/
        stage("Remove Container"){
            steps{
                sh "docker stop ${env.containerName}${env.BUILD_NUMBER-1}"
                sh "docker rm ${env.containerName}${env.BUILD_NUMBER-1}"
            }
        }
        stage("Build Images"){
            steps{
                sh "docker build -t ${env.imageName} ."
                sh "docker tag ${env.imageName} ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Push Images"){
            /*
            steps{
                sh "docker login -u xxxx -p xxxx" //ไม่จำเป็นไม่ควรใช้วิธีนี้ในการ Login Docker
                sh "docker push ${env.imageName}"
            }
            */
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
        /*stage("Deploy"){
            steps{
                sshagent(['uat-server']){
                    //sh "echo 'xxxx'"
                    //sh "ssh core@167.99.237.229 docker pull ${env.imageName}"
                }
            }
        }*/
        stage("Remove Images"){
            steps{
                //sh "docker rmi ${env.imageName}:1.${env.BUILD_NUMBER}"
                sh "docker rmi registry.hub.docker.com/${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Pull Images"){
            steps{
                //sh "docker pull ${env.imageName}:1.${env.BUILD_NUMBER}"
                sh "echo 'xxxx'"
            }
        }
        stage("Create Container"){
            steps{
                sh "docker run -d ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
    }
}
