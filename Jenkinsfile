node{
    
    
    def mavenHome= tool name: 'maven3.9.4'


    echo "the build number is : ${env.BUILD_NUMBER}"
        echo "the job name is : ${env.JOB_NAME}"
        echo "the branch name is: ${env.BRANCH_NAME}"
        echo "the node name is: ${env.NODE_NAME}"
        properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])


    
    stage('configuring git'){
        
        git credentialsId: 'd3d38961-1977-46a3-9bb4-69e86f0a510c', url: 'https://github.com/mourym/maven-web-application.git'

            }
    stage('maven build'){
        
        sh "$mavenHome/bin/mvn clean package"
        
    }
    /*
    stage('sonarqube'){
        
        sh "$mavenHome/bin/mvn sonar:sonar"
        
    }
    stage('uploadintonexus'){
        
        sh "$mavenHome/bin/mvn deploy"
        
        
    }
    
    stage('deployintotomcat'){
        
        sshagent(['10938d44-fadd-4baa-b3f1-cd17489599e7']) {
            
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.2.80.25:/opt/apache-tomcat-9.0.80/webapps"
            
            
        }
        
       
    }
    
     */
    
    
    
}//node 
