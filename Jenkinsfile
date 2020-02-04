
pipeline {
    agent any
    stages {
        stage('checkout repo') {
			steps {
				git url: 'https://github.com/lerndevops/samplejavaapp.git'
            }
        }
        stage('build artifact') {
			steps {
				sh 'mvn clean package'
            }
        }
       
        stage('push docker image') {
			steps {
				 sh "sudo docker login -u venkytvh -p venky048@"
                                 sh "sudo docker build -t venkytvh/javaapp ."
                                 sh "sudo docker push venkytvh/javaapp:$build_id"
			}
        }
        stage('Deploy to K8s') {
			steps {
				sh 'kubectl apply -f deploy/sampleapp-deploy-k8s.yml'
			}
        }
    }
}
