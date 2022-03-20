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

    stage('Quality gate check status'){
        timeout(time: 1, unit: 'HOURS'){
            def qg = waitForQualityGate()
            if (qg.status != 'OK'){
                error "Pipeline aborted due to quality gate failure: ${qg.status}"
            }
        }
    }

    stage('deploy war to Tomcat'){
        sshagent(['tomcat-pipeline']){
            sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.16.183:/opt/apache-tomcat-9.0.60/webapps/'
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
