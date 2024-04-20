node{
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
def mavenHome = tool name: 'maven-3.9.6'

stage('CheckoutCode'){
git branch: 'development', changelog: false, credentialsId: '0f3d9fac-a704-4411-8b4a-d533f774307f', poll: false, url: 'https://github.com/uptimecareer/maven-web-application.git'
}

stage('BuildArtifact'){
 sh "${mavenHome}/bin/mvn clean package"
}

stage('SonarQubeReport'){
 sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('UploadArtifactIntoNexus'){
 sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcat'){
sshagent(['eb7b5b5b-ab0b-4b5d-8ac6-3a3c31e5607b']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.80.37.84:/opt/tomcat9/webapps/"    
}
}

}
