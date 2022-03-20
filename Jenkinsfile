node{
    stage('SCM Checkout'){

        git branch: 'main', url: 'https://github.com/Harinath213/webapp.git'
    }

    stage('compile the code'){
        // get the maven home path
        def mvnHome = tool name: 'maven-3', type: 'maven'
        sh "${mvnHome}/bin/mvn package"
    }

    stage('sonar analysis'){
        def mvnHome = tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv(credentialsId: 'sonar-jenkins') {
            sh "${mvnHome}/bin/mvn sonar:sonar" 
       }
    }

    stage('Email Notification'){
       mail bcc: '', body: '''Hi, 
       Welcome, Jenkins Pipeline jobs alert.

       Regards,
       Hari

       ''', cc: '', from: '', replyTo: '', subject: 'scripted pipeline job', to: 'haridevops190@gmail.com'


    }   
}
