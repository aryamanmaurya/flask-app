pipeline {
    agent any
    parameters {
        string(name: 'tag', defaultValue: 'latest', description: 'docker image tag version')
    }
    
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
                sh "docker image tag krishna:${params.tag} ${env.dockerHubUser}/krishna:${params.tag}"
                sh "docker push ${env.dockerHubUser}/krishna:${params.tag}"
                }
            }
        }
    }
}
