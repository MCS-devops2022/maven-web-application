node{
    
def mavenHome = tool name: "Maven3.8.5"  
    
//Checkout stage
stage('CheckoutCode'){
git branch: 'development', credentialsId: '224cc402-4f28-451b-b694-e13202a74868', url: 'https://github.com/MCS-devops2022/maven-web-application.git'
}

//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
} 

//Generate SonarQube Report
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn sonar:sonar"
} 

//Upload Artifact into Artifactory Repo
stage('UploadartifactstoNexus'){
sh "$mavenHome/bin/mvn deploy"
}

//Depoly App into Tomcat Server
stage('DeployAppintoTomcat'){
sshagent(['06e244c2-e9e6-49f6-bb11-85f5dfb806d6']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.28.218:/opt/apache-tomcat-9.0.59/webapps"
} 
}

}//Node closing
