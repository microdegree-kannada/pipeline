pipeline {
    agent any
    
    tools{
        maven '3.8.3'
    }
    
    environment {
                SERVICE_BRANCH = "master"
            }
            
    stages {
        stage('checkout') {
            steps {
                echo "the branch is ${params.branch}"
                git branch: 'main', url: 'https://github.com/microdegree-kannada/mvn_jar.git'
                }
            }
        stage('compile and build'){
            when {
	            expression {
	            	return BRANCH == 'main';
                              }
                 }
            steps{
                sh "mvn clean install"
                sh 'echo "The environment variable is ${SERVICE_BRANCH}"'
                }
            }
        stage('Test'){
            steps{
                sh "mvn test"
             }
        }
    }
    post { 
        always { 
            junit '**/target/surefire-reports/TEST-com.microdegree.AppTest.xml'
        }
    }
}

