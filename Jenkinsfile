pipeline {
    
    agent {
        label 'agent-vm'
    }
    
    environment{
        IMAGE_NAME = "mon-image-site-web"
        CONTENEUR_NAME = "mon-conteneur-site-web"
    }


    stages {
        stage('Build'){
            steps {
                echo "Building the project..."
                sh "docker build -t $IMAGE_NAME ."
                echo "Build completed."
            }
        }
        stage('Stop container'){
            steps {
                echo "Stop containers if they are running..."
                sh "docker stop $CONTENEUR_NAME || true"
            }
        }
        stage('Remove old container'){
            steps {
                echo "Remove old containers if they exist..."
                sh "docker rm $CONTENEUR_NAME || true"
            }
        }
        stage('Run new container'){
            steps {
                echo "Run the new container..."
                sh "docker run -d --name $CONTENEUR_NAME -p 9000:80 $IMAGE_NAME"
                echo "Container is running."
            }
        }
    }
}

