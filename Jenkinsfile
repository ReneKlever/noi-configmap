pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                kubectl create configmap my-noi-objserv-agg-primary-config --from-file ncoprimary-configmap.yaml -o yaml --dry-run | kubectl apply -f -
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
                kubectl create configmap prod-noi-objserv-agg-primary-config --from-file=ncoprimary-configmap.yaml
            }
        }
    }
}
