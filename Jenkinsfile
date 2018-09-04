node 
{
    notify (' Jenkins started..')
stage('checkout')
{
checkout([$class: 'GitSCM',
branches: [[name: '*/master']],
doGenerateSubmoduleConfigurations: false,
extensions: [], 
submoduleCfg: [],
userRemoteConfigs: [[url:'https://github.com/vincentFurtado/Devops.git']]])
}
    notify (' Build started.. ')
stage('maven build')
{

sh 'mvn clean package'
}

notify (' Creating archive.. ')

stage('archive')
{

archiveArtifacts 'target/Helloworldwebapp.war'
}

notify (' Waiting for Approval ')
input 'Deploy to Production server ? '
stage('deploy')
{

    sh 'cp target/Helloworldwebapp.war /opt/tomcat/webapps'
}
notify (' Deployed..')

}


def notify (status){
    mail bcc: '',
body: 'Jenkins Mail',
cc: '', from: '',
replyTo: '',
subject: 'Jenkins Mail ',
to: 'devops68@gmail.com'
}

