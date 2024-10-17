pipeline {
    agent any
    stages {
        stage("hello message") {
            steps {
                echo "Hello from DevOps team."
                echo "Have a nice day."
            }
        }
        stage("Checkout the code.") {
            steps {
                echo "checking out the code..."
                git url: "https://github.com/aryamanmaurya/flask-app", branch: "main"
                echo "code cloning sucessful."
            }
        }
        stage("Build the image of the Code.") {
            steps {
                sh "docker build -t krishna:latest ."
                echo "image build sucessful."
            }
        }
        stage("push image to dockerHub") {
            steps {
                withCredentials([usernamePassword('credentialsId': "dockerHubCred",
                passwordVariable:"dockerHubPass",
                usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag krishna:latest ${env.dockerHubUser}/krishna:$tag"
                sh "docker push ${env.dockerHubUser}/krishna:$tag"
                }
            }
        }
    }
}
