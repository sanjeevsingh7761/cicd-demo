pipeline {
    agent any
    tools{
        maven 'maven_3_9_9'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sanjeevsingh7761/cicd-demo']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh '/usr/local/bin/docker build -t sanjeevsingh7761/devops-integration .'
                }
            }
        }

        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh '/usr/local/bin/docker login -u sanjeevsingh7761 -p ${dockerhubpwd}'



                   sh '/usr/local/bin/docker tag sanjeevsingh7761/devops-integration sanjeevsingh7761/devops-integration:latest'




}
                   //sh '/usr/local/bin/docker push cicddemo/devops-integration:latest'
                   // Push to Docker Hub
                   sh '/usr/local/bin/docker push sanjeevsingh7761/devops-integration:latest'
                }
            }
        }
        //stage('Deploy to Kubernetes') {
            //steps {
               // withKubeConfig([credentialsId: 'k8s-kubeconfig']) {
             //       sh '/opt/homebrew/bin/kubectl apply -f deploymentservice.yaml --validate=false'
           //     }
         //   }
       // }

        }
    }