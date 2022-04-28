//Get the code from Github Repo
node{
echo "Job name is: ${env.JOB_NAME} "
echo "Node Name is : ${env.NODE_NAME} "
def mavenHome =tool name:'maven3.8.5'
stage ('checkoutcode'){
git branch: 'development', credentialsId: 'eb54a3b9-213b-41f4-a5e9-3c3cae4756ac', url: 'https://github.com/Joseph150580/maven-web-application.git'

}
// Do the build by using maven Build tool
stage ('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

// Excute the sonarqube report
stage ('ExcuteSonarqubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}
// Upload Artifacts in to Artifactory Repo
stage ('UploadArtifactsiInToNexus'){
sh "${mavenHome}/bin/mvn deploy"
}
//Deploy application in to TomCat server
stage('DeployApplicationInToTomcatServer'){
sshagent(['4e5d12fd-4220-4a75-9781-a4ff2dfca5c4']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.19.178:/opt/apache-tomcat-9.0.62/webapps"
}

}
}


