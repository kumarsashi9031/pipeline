pipeline {
    agent {
        label 'slave1'
    }
    stages {
        stage('Git-Checkout') { 
            steps {
                echo "checking out from git repo";
                git 'https://github.com/javaparser/javaparser-maven-sample.git'
                
                // 
            }
        }
        stage('Build') { 
            steps {
                sh 'mvn clean install'
                
                // 
          }
        }
        stage('email notification') {
            steps {
                emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        
            }    
        }
        stage('deployment of an agent'){
            steps {
                sshagent(['4a2572d4-8cde-4d54-b399-e767fd7c4413']) {
                   sh "scp target/**.jar ubuntu@ec2-52-90-87-94.compute-1.amazonaws.com:/home/ubuntu/slave3"
                }   
            }   
        }
        
    } 
    post('archive the artifact') {
        success {
            archiveArtifacts artifacts: 'target/**.jar'
            
        } 
    }
        
}