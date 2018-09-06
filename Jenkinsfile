node 
{
stage('checkout')
{
checkout([$class: 'GitSCM',
branches: [[name: '*/master']],
doGenerateSubmoduleConfigurations: false,
extensions: [], 
submoduleCfg: [],
userRemoteConfigs: [[url:'https://github.com/vincentFurtado/Devops.git']]])
}
stage('maven build')
{

sh 'mvn clean package'
}


stage('archive')
{

archiveArtifacts 'target/Helloworldwebapp.war'
}

input 'Deploy to Production server ? '
stage('deploy')
{

    sh 'cp target/Helloworldwebapp.war /opt/tomcat/webapps'
}
notify ('Cheers !!! Deployed..')

}

def notify(status) {
  mail (
        body:"""${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':
                 Check console output at, 
                 href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]""",
        cc: '', 
        subject: """JenkinsNotification: ${status}:""", 
        to: 'devops68@gmail.com'  
       ) 
 }

