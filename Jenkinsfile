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
                deploy("dev")
            }
        }
         stage('test-dev') {
            steps {
                run_api_tests("dev")
            }
        }
        //  stage('deploy-stg') {
        //     steps {
        //         deploy("stg")
        //     }
        // }
        //  stage('test-stg') {
        //     steps {
        //         run_api_tests("stg")
        //     }
        // }
        //  stage('deploy-prod') {
        //     steps {
        //         deploy("prod")
        //     }
        // }
        //  stage('test-prod') {
        //     steps {
        //         run_api_tests("prod")
        //     }
        // }
        
    }

}

def build_docker_image(){
    echo "Building a Docker Image from python-greetings repository."
    sh "docker build -t lynnmal/python-greetings-app:latest ."

    echo "Pushing image to a docker registry."
    sh "docker push lynnmal/python-greetings-app:latest"
}

def deploy(String environment){
    echo "Deployment triggered on ${environment} env."

    echo "Pulling latest python-greetings-app Image from Docker Hub"
    sh "docker pull lynnmal/python-greetings-app:latest"

    echo "Stopping previous Application service."
    sh "docker compose stop greetings-app-${environment}"

    echo "Removing prevoius Application container."
    sh "docker compose rm greetings-app-${environment}"

    echo "Creating a new Application container."
    sh "docker compose up -d greetings-app-${environment}"
}

def run_api_tests(String environment){
     echo "API Tests triggered on ${environment} env."

     echo "Pulling latest api-tests Image from Docker Hub."
     sh "docker pull lynnmal/api-tests"

     echo "Running container which is going to execute tests."
     sh "docker run --network=host --rm lynnmal/api-tests:latest run greetings greetings_${environment}"
}