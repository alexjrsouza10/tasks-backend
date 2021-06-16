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
    }
}