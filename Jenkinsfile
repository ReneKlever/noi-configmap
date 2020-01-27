pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'kubectl create configmap my-noi-objserv-agg-primary-config --from-file agg-p-props-append --from-file agg-p-sql-extensions -o yaml --dry-run | kubectl apply -f -'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            environment {
                RELEASE ="""${sh(
                         returnStdout: true,
                         script: 'kubectl get pods -n noi |grep ncoprimary|cut --fields=1,2 --delimiter=-'
                )}"""
                NOIRELEASE = RELEASE.trim()
            }
            steps {
                echo 'Deploying....'
                sh 'kubectl create configmap ${NOIRELEASE}-objserv-agg-primary-config --from-file agg-p-props-append --from-file agg-p-sql-extensions -o yaml --dry-run | kubectl apply -f -'
                sh 'kubectl delete pod ${NOIRELEASE}-ncoprimary-0'
            }
        }
    }
}
