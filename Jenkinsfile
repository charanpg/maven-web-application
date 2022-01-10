node
{
    def maven = tool name: "maven3.8.4"

stage('checkoutcode')
{
    git branch: 'development', credentialsId: 'a968376d-026f-4156-b665-0c0fa2b3c542', url: 'https://github.com/charanpg/maven-web-application.git'
}
stage('build')
{
    sh "${maven}/bin/mvn clean package"
}
stage('sqreport')
{
    sh "${maven}/bin/mvn clean sonar:sonar"
}
stage('uploadartifact')
{
    sh"${maven}/bin/mvn clean deploy"
}
stage('deploy')
{
    sshagent(['c0b9e938-ef0a-4b89-b97d-73c942575bbd']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.141.17.54:/opt/apache-tomcat-9.0.56/webapps/"
}
}
stage('emailnotification')
{
    emailext body: '''build done

regards
charanpg''', subject: 'build done', to: 'saicharan1222@gmail.com'
}
}
