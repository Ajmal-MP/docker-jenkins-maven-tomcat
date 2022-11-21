pipeline {
    agent any

    stages {
        
        stage('getting code from git') {
            steps {
                git branch: 'main', url: 'https://github.com/Ajmal-MP/Maven-Web-Project.git'
            }
        }
        
        stage('maven build') {
            //agent { docker 'maven:3.3.3' }
            steps {
                dir('/var/jenkins_home/workspace/docker') {
                         sh "docker run -it --rm --name my-maven -v "$(pwd)":/usr/local/mymaven -w /usr/src/mymaven mymaven mvn -e clean install"
                         //sh "pwd"
                         //sh 'mvn clean package'
                    }
            }
        }
        
        stage ('tomcat deployment') {
            steps {
                dir('/var/jenkins_home/workspace/docker') {
                    deploy adapters: [tomcat8(credentialsId: '674285a7-f187-4053-97e7-c2cba1970acd', path: '', url: 'http://18.181.253.239:8081/')], contextPath: 'maven-sample', war: '**/*.war'
                }
                
                
            }
        }
        
    }
}

    
