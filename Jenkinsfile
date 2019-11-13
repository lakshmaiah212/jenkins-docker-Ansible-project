pipeline{
    agent any
    stages{
        stage('SCM-Checkout'){
            steps{
                git 'https://github.com/yankils/hello-world.git'
            }
           
        }
        stage('code build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('copy war file to docker-host'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Dockerhost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/dockeradmin; docker build -t jenkinscontainer . ;
                docker run -dit --name jenkinsdocker -p 8080:8080 jenkinscontainer''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: 'webapp/target/webapp.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
      
    }
}
