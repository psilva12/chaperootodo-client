pipeline{
        agent any
        environment {
            app_version = 'v1'
            rollback = 'false'
        }
        stages{
            stage('Build Image'){
                steps{
                    script{
                        if (environment.rollback == 'false'){
                            image = docker.build("palinhesosilva/chaperoo-frontend")
                        }
                    }
                }          
            }
            stage('Tag & Push Image'){
                steps{
                    script{
                        if (environment.rollback == 'false'){
                            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
                                image.push("${environment.app_version}")
                            }
                        }
                    }
                }          
            }
            stage('Deploy App'){
                steps{
                    sh "docker-compose up -d"
                }
            }
        }    
}
