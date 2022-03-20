node{
    stage('SCM Checkout'){
        git 'https://github.com/Harinath213/webapp.git'
    }

    stage('compile the code'){
        // get the maven home path
        def mvnHome = tool name: 'maven-3', type: 'maven'
        sh "${mvnHome}/bin/mvn package"
    }
}