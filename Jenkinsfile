pipeline {
    agent any
    
    stages {
    
         stage("build") {
             steps {
             sh "./mvnw package"
             }
         }
         
         stage("capture") {
             steps {
             archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
             jacoco()
             junit '**/target/surefire-reports/TEST*.xml'
             }
         }
    }
    
    post {
        always {
            //email body
            emailext body: '${env.BUILD_URL}\n${currentBuild.absoluteURL}', 
            to: 'denis.mugisha@akelius.com',
            recipientProviders: [previous()], 
            subject: '"${currentBuild.currentResutl}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]'
        }
    }
}
