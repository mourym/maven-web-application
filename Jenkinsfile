node{
    
    
    def mavenHome= tool name: 'maven3.9.4'


    echo "the build number is : ${env.BUILD_NUMBER}"
        echo "the job name is : ${env.JOB_NAME}"
        echo "the branch name is: ${env.BRANCH_NAME}"
        echo "the node name is: ${env.NODE_NAME}"
        properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])
        buildName 'dev-#${BUILD_NUMBER}'

def sendSlackNotifications(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications 
//add parameter channel to change chanell name
  slackSend (color: colorCode, message: summary,channel:'#citibank')
}

    

    try{
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
    }//try closing

    catch(e){
        currentBuild.result='FAILED'

        
    }//catch closing
    finally{

        sendSlackNotifications(currentBuild.result)
    }
    
    
    
}//node 
