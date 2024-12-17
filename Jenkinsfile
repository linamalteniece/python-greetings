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
        //  stage('deploy-dev') {
        //     steps {
        //         deploy("DEV")
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

// def deploy(String environment){
//     echo "Deployment triggered on ${environment} env."

//     echo "Pulling latest puthon-greetings-app Image from Docker Hub"
//     sh "docker pull lynnmal.python-greetings-app:latest"

//     echo "Stopping previous Application service."
//     sh "docker compose stop greetings-app-${environment}"

//     echo "Removing prevoius application container."
//     sh "docker compose rm api-tests-${environment}"

//     echo "Creating a new Application container."
//     sh "docker compose up -d api-tests-${environment}"
// }