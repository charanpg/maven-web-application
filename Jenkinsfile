pipeline 
{
    agent any
    tools {
  maven 'maven3.8.4'
}
triggers {
    pollSCM '* * * * *'
}
options {
  timestamps()
}
    stages 
    {
        stage('checkoutcode')
        {
            steps
            {
                git branch: 'stage', credentialsId: '0c2ed8a7-f3d8-4495-8c6d-cdc60a5d1384', url: 'https://github.com/charanpg/maven-web-application.git'
            }
        }
        stage('build')
        {
            steps
            {
                sh "mvn clean package"
            }
        }
        stage('sqreport')
        {
            steps {
                sh "mvn sonar:sonar"
            }
        }
        stage('uploadtonexus')
        {
            steps
            {
                sh "mvn clean deploy"
            }
        }
        stage('deploytotomcat')
        {
            steps
            {
                sshagent(['6e56270b-09db-4fab-b879-dffadce0ad05']) {
    sh "scp -o stricthostkeychecking=no target/maven-web-application.war ubuntu@13.59.76.174:/opt/apache-tomcat-9.0.62/webapps" 
     }
            }
        }
    } // stages closing
    post {
  always {
    emailext body: 'kani', subject: 'emo', to: 'saicharan1222@gmail.com'
  }
  success {
    emailext body: 'kani', subject: 'emo', to: 'saicharan1222@gmail.com'
  }
  failure {
    emailext body: 'kani', subject: 'emo', to: 'saicharan1222@gmail.com'
  }
}


} // pipeline closing
