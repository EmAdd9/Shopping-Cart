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
        stage('Maven Compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('Sonarqube Analysis') {
            steps {
                 withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=EKART \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=EKART '''
                }
            }    
        }
        stage('Trivy FS') {
            steps {
                sh "trivy fs ."
            }
        }
        stage('OWASP-FS-Scan') {
            steps {
               dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'owasp'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Package') {
            steps {
                sh "mvn package -DskipTests=true"
            }
        }
        stage('Deploy to Nexus') {
            steps {
                withMaven(globalMavenSettingsConfig: 'maven-settings') {
                   sh "mvn deploy -DskipTests=true"   
                }
            }
        }





    
    }
}
