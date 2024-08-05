node{
// properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
def mavenHome = tool name: 'maven-3.9.8'

    echo "The Job name is: ${env.JOB_NAME}" 
    echo "The Build numebr is: ${env.BUILD_NUMBER}"
    echo "The node name is: ${env.NODE_NAME}"

stage('Checkout'){
git branch: 'development', changelog: false, credentialsId: '0f3d9fac-a704-4411-8b4a-d533f774307f', poll: false, url: 'https://github.com/uptimecareer/maven-web-application.git'
}

stage('BuildArtifact'){
 sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('SonarQubeReport'){
 sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('UploadArtifactIntoNexus'){
 sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcat'){
sshagent(['eb7b5b5b-ab0b-4b5d-8ac6-3a3c31e5607b']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.84.121.239:/opt/tomcat9/webapps/"    
}
}

stage('SendEmailNotification'){
mail bcc: '', body: '''Regards,
Uptime Career''', cc: '', from: '', replyTo: '', subject: 'Build Over', to: 'uptimecareer@gmail.com'
}
*/
}
