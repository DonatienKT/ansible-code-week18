pipeline{
    agent any

    stages{
        stage("zip the file"){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
        }
        
        stage('upload artifacts to jfrog'){
            steps{
                sh 'curl -uadmin:AP6Q75MQXFQHggFWzUUVfo8HfEy -T \
                ansible-${BUILD_ID}.zip \ 
                "http://52.202.32.92:8081/artifactory/ansible-doc/ansible-${BUILD_ID}.zip"'
                
            }
        }
    }
}