pipeline {
    agent any
   
   
    stages{
        stage("clone Code"){
            steps {
                echo "Cloning the code"
                git url: "https://github.com/prashantsagar7/notes.git", branch :"main"
                
            }
        }
        stage("build"){
            steps {
                echo "Building the image"
                sh 'docker build -t my-notes-app .'
                
            }
            
        }
        
        stage("Push to Docker Hub") {
    steps {
        echo "Pushing the image to Docker Hub"
        withCredentials([usernamePassword(credentialsId: "dokerhub", passwordVariable: "dockerhubpass", usernameVariable: "dockerhubuser")]) {
            sh "docker tag my-notes-app ${env.dockerhubuser}/my-notes-app:latest"
            sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
            sh "docker push ${env.dockerhubuser}/my-notes-app:latest" 
            
        }
    }
}

        
        stage('Deploy Container') {
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }   
}
