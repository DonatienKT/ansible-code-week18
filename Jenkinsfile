pipeline{
    agent any

    stages{
        stage("zip the file"){
            steps{
                sh 'rm -rf *.zip || echo ""'
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
        }
        
        stage('upload artifacts to jfrog'){
            steps{
                sh 'curl -uadmin:AP6Q75MQXFQHggFWzUUVfo8HfEy -T ansible-${BUILD_ID}.zip "http://52.202.32.92:8081/artifactory/ansible-doc/ansible-${BUILD_ID}.zip"'
                
            }
        }
        stage('publish to ansible server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'anbsible-server', transfers: [sshTransfer(cleanRemote: false, \
                excludes: '', execCommand: 'ls', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, \
                patternSeparator: '[, ]+', remoteDirectory: '/ansible-dev', remoteDirectorySDF: false, removePrefix: '', \
                sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }
        }
    }
}