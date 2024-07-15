pipeline{
    agent any
    stages{
        stage(build maven){
            steps{
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }
         stage(copy Artifacts){
            steps{
               sh 'pwd'
               sh 'cp -r target/*.jar docker'
           }
        }
        stage(unit tests){
            steps{
               sh 'mvn unit test'
           }
       }
        stage (Build Docker Image){
            steps{
               script{
                 def customImage = docker.build(iran141/petclinic:$"{BUILD_NUMBER}", .docker)
                 docker.withRegistry('https://registry.docker.hub.com') 'dockerhub'
                 customImage.push
            }
        }
        stage (build on kubernetes){
            steps{
                withKubeConfig([credentialsId: kubeconfig])
                sh 'pwd'
                sh 'cp -r helm/* .'
                sh 'ls -ltrh'
                sh 'pwd'
                sh '/usr/local/bin/heml upgrade --install p'
            }
        }
    }
    }
}