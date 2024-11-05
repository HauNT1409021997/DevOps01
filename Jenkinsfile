pipeline {
    agent none
    stages {
        stage('Build Node.js Project') {
            agent { label 'nodejs-slave-8f3f9c84' }
            steps {
                echo 'Building Node.js project...'
                sh 'npm install --prefix /home/reactApp'
                sh 'npm run build --prefix /home/reactApp'
            }
        }
        stage('Deploy React App') {
            agent { label 'nodejs-slave-8f3f9c84' }
            steps {
                echo 'Starting React.js app...'
                sh 'cd /home/reactApp && ./deliver.sh &'
            }
        }
        stage('Build Java Project') {
            agent { label 'java-slave-c44b877d' }
            steps {
                echo 'Building Java project...'
                sh 'mvn clean package -f /home/javaApp/pom.xml'
            }
        }
        stage('Deploy Java App') {
            agent { label 'java-slave-c44b877d' }
            steps {
                echo 'Starting Java app with Maven...'
                sh 'cd /home/javaApp && mvn spring-boot:run &'
            }
        }
    }
}
