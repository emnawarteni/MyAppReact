
pipeline {
    agent any

    stages {
        stage('Checkout GitHub') {
            steps {
                bat 'if exist MyAppReact rmdir /s /q MyAppReact'
                bat 'git clone https://github.com/emnawarteni/MyAppReact.git'
            }
        }

        stage('Build Server Image') {
            steps {
                bat '"C:\\Users\\LENOVO\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t mern-server:latest MyAppReact\\Server'
            }
        }

        stage('Build Client Image') {
            steps {
                bat '"C:\\Users\\LENOVO\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t mern-client:latest MyAppReact\\Client'
            }
        }
    }
}
