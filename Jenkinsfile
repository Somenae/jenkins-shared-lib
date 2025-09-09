pipeline {
    agent any
    
    triggers {
        githubPush()
    }

    parameters {
        choice(name: 'env', choices: ['dev', 'prod'], description: 'Select environment')
    }

    stages {
        stage('Determine Environment') {
            steps {
                script {
                    def targetCluster = ''
                    if (params.env == 'prod') {
                        targetCluster = 'cluster kube de production'
                    } else if (params.env == 'dev') {
                        targetCluster = 'cluster kube de dev'
                    }
                    echo "Target Cluster: ${targetCluster}"
                    env.TARGET_CLUSTER = targetCluster
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Test...'
            }
        }
        stage('Trigger next job') {
            steps {
                script {
                    build job: 'Pipeline-CD', parameters: [string(name: 'TARGET_CLUSTER', value: env.TARGET_CLUSTER)]
                }
            }
        }
    }
}