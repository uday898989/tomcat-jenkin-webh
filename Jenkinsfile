pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/uday898989/tomcat-jenkin-webh.git']]])
            }
        }
        
        stage('Clean') {
            steps {
               sh "mvn -Dmaven.test.failure.ignore=true clean"
            }
        }
        
        stage('Validate') {
            steps {
                sh "mvn validate"
            }
        }
        
        stage('Compile') {
            steps {
                sh ('mvn compile');
            }
        }
        
        stage('Test') {
            steps {
                sh ('mvn test');
            }
        }
        
        stage('Package') {
            steps {
                sh ('mvn package');
            }
        }
        
        stage('Verify') {
            steps {
                sh ('mvn verify');
            }
        }
        
        stage('Install') {
            steps {
                sh ('mvn install');
            }
        }
        stage('deploy') {
            steps {
                sshagent(['deploy_user']) {
                   sh "scp -o StrictHostKeyChecking=no -T target/**.war target/01-maven-web-app.war ubuntu@44.203.51.104:/opt/tomcat/webapps"
                    
                        }
            }
        }
          
    }
}
