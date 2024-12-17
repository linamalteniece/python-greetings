pipeline{
    agent any
    triggers {
        pollSCM('*/1 * * * *')
    }
    stages{
        stage('build-docker-image') {
            steps {
                build_docker_image()
            }
        }
         stage('deploy-dev') {
            steps {
                deploy("DEV")
            }
        }
    }

}

def build_docker_image(){
    echo "Building a Docker Image."
    sh "docker build -t lynnmal/api-tests:latest ."

    echo "Pushing image to a docker registry."
    sh "docker push lynnmal/api-tests:latest"
}

def deploy(String environment){
    echo "Deployment triggered on ${environment} env."
    // String lowercaseEnv  = environment.toLowerCase()
    sh "docker compose stop api-tests-${environment}"
    sh "docker compose rm api-tests-${environment}"
    sh "docker compose up -d api-tests-${environment}"
}