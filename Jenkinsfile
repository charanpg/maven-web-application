node
{
    def mhd = tool name: "maven3.8.5"
    stage ('checkoutcode')
    {
        git branch: 'development', credentialsId: '6c81c4e5-88ee-4655-923b-48c2b534bae3', url: 'https://github.com/charanpg/maven-web-application.git'
    }
    stage ('build')
    {
        sh "${mhd}/bin/mvn clean package"
    }
    stage ('sqreport')
    {
        sh "${mhd}/bin/mvn sonar:sonar"
    }
    stage ('Uploadintonexus')
    {
        sh "${mhd}/bin/mvn clean deploy"
    }
    stage ('DeployintoTomcat')
    {
        sshagent(['024a5610-ef4e-42eb-8b8c-ec0500ca1eb2']) {
    sh "scp -o stricthostkeychecking=no target/maven-web-application.war ubuntu@13.58.145.101:/opt/tomcat/webapps/"
}
    }
    /*
    stage ('Sendemailnotification')
    {
        emailext body: '''Notify Status.

Regards,
Charan
1039612.''', replyTo: 'saicharan1222@gmail.com', subject: 'Email Notification.', to: 'saicharan1222@gmail.com'
    } */
}
