pipeline {
    agent any
    
    stages {       
        stage ('Docker_Build') {
            steps {
                sh'''
                    # Build the image
                    COMMIT_ID=$(git rev-parse --short HEAD)
                    echo 'Building the docker image with commit ID: '
                    docker build -t "sample-app:${COMMIT_ID}" .
                '''
            }
        }
    }
}
        
        stage ('Deploy_K8S') {
             steps {
                     withCredentials([string(credentialsId: "argocd-token", variable: 'ARGOCD_AUTH_TOKEN')]) {
                        sh '''
                        ARGOCD_SERVER="argocd"
                        APP_NAME=""
                        CONTAINER="k8s-debian-test"
                        COMMIT_ID=$(git rev-parse --short HEAD)
                        echo 'Building the docker image with commit ID: '
                        # Customize image 
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app set $APP_NAME --kustomize-image $IMAGE_DIGEST                       
                        # Deploy to ArgoCD
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app sync $APP_NAME --force
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app wait $APP_NAME --timeout 600
                        '''
               }
            }
        }