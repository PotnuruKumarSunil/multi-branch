pipeline{
    agent{
        label "linuxbuildnode"
    }
    
    stages{
        stage('SCM'){
            steps{
                git 'https://github.com/PotnuruKumarSunil/jenkins-docker-maven-java-webapp.git'
            }
        }
        stage('Build by Maven'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh "sudo docker build -t sunilpotnuru/javaweb:${BUILD_TAG} ."
                //sh 'whoami'
            }
        }
        stage('Push image to Docker Hub'){
            steps{
                withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'DOCKER_HUB_PASS_CODE')]) {
                    sh "sudo docker login -u sunilpotnuru -p $DOCKER_HUB_PASS_CODE docker.io"
                }
                sh "sudo docker push sunilpotnuru/javaweb:${BUILD_TAG}"
            }
        }
        stage('Deploy webApp in Dev Env'){
            steps{
                sh 'sudo docker rm -f myjavaapp'
                sh "sudo docker run -d -p 8080:8080 --name myjavaapp sunilpotnuru/javaweb:${BUILD_TAG}"
            }
        }
        /*
        stage('Deploy webApp in QA Env'){
            steps{
                sshagent(['QA_ENV_SSH_CRED']) {
                    // X.X.X.X is the QA env ip address
                    // make sure you have docker installed in QA env
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@X.X.X.X docker rm -f myjavaapp"
                    sh "ssh ec2-user@X.X.X.X docker run -d -p 8080:8080 --name myjavaapp sunilpotnuru/javaweb:${BUILD_TAG}"
                }
            }
        }
        */
        
        /*
        stage('QAT test stage'){
            steps{
                // below is a sample test case and X.X.X.X is QA env ip address
                sh 'curl --silent http://X.X.X.X:8080/path/to/the/website | grep India'
            }
        }
        */
        
        
        //Below should be done only after test stage here docker is exiting immediately so i hv done like this
        stage('Manual Approval Stage'){
            steps{
                input(message: "Release to ProdEnv?")
            }
        }
    
        stage('Deploy webApp in ProdEnv'){
            steps{
                sshagent(['QA_ENV_SSH_CRED']) {
                    // 35.175.149.164 is the  ProdEnv ip address,update it everytime
                    // make sure you have docker installed in QA env
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@35.175.149.164 sudo docker rm -f myjavaapp"
                    sh "ssh ec2-user@35.175.149.164 sudo docker run -d -p 8080:8080 --name myjavaapp sunilpotnuru/javaweb:${BUILD_TAG}"
                }
            }
        }
        
    }
    
    
}