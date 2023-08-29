pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('SCM checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sudhakarbastawade2303/spring-boot-war-example.git']])
            }
        }
	stage('Sonar stage') {
            steps {
                echo "running sonar scan"
		}
        }
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('deploy') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://15.206.82.37:8080')], contextPath: '/app', war: '**/*.war'
            }
        }    
    }
	post {
          success {
             mail to: devops.classes.online@gmail.com, subject: ‘The Pipeline success :(‘
    }
  }
}


