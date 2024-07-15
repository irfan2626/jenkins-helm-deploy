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
<<<<<<< HEAD
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
=======
                script {
                    def customImage = docker.build("irfan2626/petclinic:${env.BUILD_NUMBER}", "./docker")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    customImage.push()    
                }
>>>>>>> 18795c891bec8fb22992d1951585d3dda379e796
            }
        }
        stage (build on kubernetes){
            steps{
                withKubeConfig([credentialsId: kubeconfig])
                sh 'pwd'
                sh 'cp -r helm/* .'
                sh 'ls -ltrh'
                sh 'pwd'
<<<<<<< HEAD
                sh '/usr/local/bin/heml upgrade --install p'
            }
=======
                sh '/usr/local/bin/helm upgrade --install petclinic-app petclinic --set image.repository=irfan2626/petclinic --set image.tag=${BUILD_NUMBER}'
>>>>>>> 18795c891bec8fb22992d1951585d3dda379e796
        }
    }
    }
}
