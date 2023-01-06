node{


def mavenHome = tool name: "maven 3.8.6"

echo "The Job name is: ${env.JOB_NAME}"
echo "The Nod ename is: ${env.NODE_NAME}"
echo "The Build Number is: ${env.BUILD_NUMBER}"
echo "The Jenkins Home directory is: ${JENKINS_HOME}"

stage('CheckoutCode'){
git branch: 'master', credentialsId: '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', url: 'https://github.com/BalajNaidu-7013/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('UploadArtifactsIntoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}

stage('DeployAppIntoTomcatServer'){
sshagent(['dd322509-fcdb-4679-ac54-7251c84f2f3e']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@43.205.143.71:/opt/apache-tomcat-9.0.70/webapps/" 
}
}

}

