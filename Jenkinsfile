pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'kubectl delete configmap dev-noi-objserv-agg-primary-config'
                sh 'kubectl create configmap dev-noi-objserv-agg-primary-config --from-file ncoprimary-configmap.yaml'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'kubectl delete configmap prod-noi-objserv-agg-primary-config'
                sh 'kubectl create configmap prod-noi-objserv-agg-primary-config --from-file ncoprimary-configmap.yaml'
            }
        }
    }
}
