pipeline {
    agent any
    
    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'feature1', url: 'https://github.com/EmAdd9/Shopping-Cart.git'
            }
        }


    
    }
}
