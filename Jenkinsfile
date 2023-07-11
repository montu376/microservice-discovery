pipeline{
    agent any
    
    stages{
        stage('Building Image and dockerzing it'){
            agent {
                label 'montuUbuntu'
            }
            steps {
                sh 'mvn package -DskipTests'
            }

            post{
                success{
                    archiveArtifacts artifacts: 'target/*.jar'
                    
                }        
            }
        } 

        stage('docker push'){
            agent {
                label 'montuUbuntu'
            }
            steps {
                sh 'docker build -t montud/microservice-discovery:latest .'
                sh 'docker push montud/microservice-discovery:latest'
            }
        }


        stage('Kubernates deploy'){
            steps {
                bat 'C:\\Users\\coolm\\kubectl.exe apply -f deploy.yml'
            }
        }
    }
    


}