pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                kubectl delete configmap dev-noi-objserv-agg-primary-config
                kubectl create configmap dev-noi-objserv-agg-primary-config --from-file ncoprimary-configmap.yaml
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
                kubectl delete configmap prod-noi-objserv-agg-primary-config
                kubectl create configmap prod-noi-objserv-agg-primary-config --from-file ncoprimary-configmap.yaml
            }
        }
    }
}
