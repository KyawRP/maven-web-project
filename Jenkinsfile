pipeline {
    agent any 
     tools {
        maven "Maven 3.8.6" // the name you have given the JDK installation in Global Tool 
    }
    stages {
        
        stage("clone the git") {
            steps {
                echo "Cloning the git"
                git branch: 'master', url: 'https://github.com/KeyonGenesis/jenkins-maven-sonarqube'
                echo "Git cloned"
            }
        }
        
        stage("Building Using Maven"){
            steps{
                script {
                    sh 'mvn --version'
                    println "Maven building"
                    sh 'mvn clean package'
                    println "build Succesfully"
                }
            }
        }
        
        stage('SonarQube Quality Gate') {
            environment {
                scannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-sddo-rp', installationName: 'Staging SonarQubeScanner') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
        
            }
        }
         
       
        //  stage("Quality gate") {
        //     steps {
        //         script {
        //             println "Waiting for the QualityGate Check"
        //                 def qg = waitForQualityGate()
        //                 if (qg.status != 'OK') {
        //                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
        //                 }
        //             }
        //     }
        // }
    }
}
