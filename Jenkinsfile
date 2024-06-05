pipeline {
    agent any

    environment {
       
        DOCKER_HUB_CREDENTIALS = '15eaf95b-322c-46d1-8d13-154f984837cd'
        DOCKER_HUB_REPO = 'anumsajid'
        REPO_URL = 'https://github.com/NUCESFAST/scd-final-lab-exam-anumsajid13'
    }

    stages {
        stage('Checkout Code - i211233') {
            steps {
                git url: "${env.REPO_URL}"
            }
        }
        
        stage('Install Dependencies - i211233') {
            steps {
                script {
                    def services = ['auth', 'classroom', 'post', 'event-bus', 'client']
                    for (service in services) {
                        dir(service) {
                            sh 'npm install'
                        }
                    }
                }
            }
        }
        
        stage('Build Docker Images - i211233') {
            steps {
                script {
                    def services = ['auth', 'classroom', 'post', 'event-bus', 'client']
                    for (service in services) {
                        dir(service) {
                            sh "docker build -t ${env.DOCKER_HUB_REPO}/${service}:latest ."
                        }
                    }
                }
            }
        }
        
        stage('Push Docker Images to Docker Hub - i211233') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', env.DOCKER_HUB_CREDENTIALS) {
                        def services = ['auth', 'classroom', 'post', 'event-bus', 'client']
                        for (service in services) {
                            sh "docker push ${env.DOCKER_HUB_REPO}/${service}:latest"
                        }
                    }
                }
            }
        }
        
        stage('Deploy and Validate - i211233') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                    sh 'docker ps'
                }
            }
        }
    }
    
}
