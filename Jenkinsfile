pipeline{
    agent any
    stages{
        stage ('Build Backend'){
            steps{
                bat'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Test'){
            steps{
                bat'mvn test'
            }
        }
        stage ('Deploy Backend') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'Tomcat_login', path: '', url: 'http://localhost:8085/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }
        stage ('API Test') {
            steps {
                dir('api-test') {
                git credentialsId: 'github_login', url: 'https://github.com/alexjrsouza10/tasks-api-test'
                bat'mvn test'
                }
            }
        }
        stage ('Deploy Frontend') {
            steps {
                dir('frontend'){
                git credentialsId: 'github_login', url: 'https://github.com/alexjrsouza10/tasks-frontend'
                bat'mvn clean package'
                deploy adapters: [tomcat8(credentialsId: 'Tomcat_login', path: '', url: 'http://localhost:8085/')], contextPath: 'tasks', war: 'target/tasks.war'
                }
            }
        }
    }
}