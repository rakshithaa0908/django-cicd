	pipeline {
	    agent any 
	    stages{
	        stage("Clone Code"){
	            steps {
	                echo "Cloning the code"
	                git branch: 'main', url: 'https://github.com/rakshithaa0908/django-notes-app.git'
	            }
	        }
	        stage("Build"){
	            steps {
	                echo "Building the image"
	                sh "docker build -t my-note-app ."
	            }
	        }
	        stage("Push to Docker Hub"){
	            steps {
	                echo "Pushing the image to docker hub"
	                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])           {
	                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
	                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
	                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
	                }
	            }
	        }
	        stage("Deploy to kubernetes") {
	            steps {
	                script {
	                    dir("notesapp") {
	                        withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
	                        sh "kubectl delete --all pods"
	                        sh "kubectl apply -f deployment.yaml"
	                        sh "kubectl apply -f service.yaml"
	                        }
	                    }
	                }
	                
	            }
	        }
	    }
	}
