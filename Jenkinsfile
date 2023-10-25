pipeline {
    agent {any}
    
    stages {       
        stage ('Docker_Build') {
            steps {
                sh'''
                    # Build the image
                    COMMIT_ID=$(git rev-parse --short HEAD)
                    echo 'Building the docker image with commit ID: '
                    docker build -t "sample-ap:${COMMIT_ID}" .
                '''
            }
        }
    }
}
        
        // stage ('Deploy_K8S') {
        //      steps {
        //              withCredentials([string(credentialsId: "jenkins-argocd-deploy", variable: 'ARGOCD_AUTH_TOKEN')]) {
        //                 sh '''
        //                 ARGOCD_SERVER="argocd-prod.example.com"
        //                 APP_NAME="debian-test-k8s"
        //                 CONTAINER="k8s-debian-test"
        //                 REGION="eu-west-1"
        //                 AWS_ACCOUNT="$ACCOUNT_NUMBER"
        //                 AWS_ENVIRONMENT="staging"

        //                 $(aws ecr get-login --region $REGION --profile $AWS_ENVIRONMENT --no-include-email)
                        
        //                 # Deploy image to ECR
        //                 docker tag $CONTAINER:latest $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest
        //                 docker push $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest
        //                 IMAGE_DIGEST=$(docker image inspect $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest -f '{{join .RepoDigests ","}}')
        //                 # Customize image 
        //                 ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app set $APP_NAME --kustomize-image $IMAGE_DIGEST
                        
        //                 # Deploy to ArgoCD
        //                 ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app sync $APP_NAME --force
        //                 ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app wait $APP_NAME --timeout 600
        //                 '''
        //        }
        //     }
        // }