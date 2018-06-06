pipeline {
    agent { label 'jenkinslave' }
    stages {
        stage('Fetch dependencies') {
        /* This stage pulls the latest nginx image from
           Dockerhub */
            steps {
                sh 'sudo docker pull nginx:latest'
          }
        }
        stage('Build docker image') {
        /* This stage builds the actual image; synonymous to
           docker build on the command line */
            steps {
            sh "sudo docker build . -t customnginx:1"
            }    
        }
        stage('Test image') {
         /* This stage runs unit tests on the image; we are
            just running dummy tests here */
            steps {
                sh 'echo "Tests successful"'
          }
        }
        stage('Push image to OCIR') {
         /* Final stage of build; Push the 
            docker image to our OCI private Registry*/
        steps {
            sh "sudo docker login -u 'cloud_pursuit_appdev/sundeep.dhall@oracle.com' -p '_F;kalk73VVd48kkMEjo' phx.ocir.io"
            sh "sudo docker tag customnginx:1 phx.ocir.io/cloud_pursuit_appdev/sdhall/nginx:custom2"
            sh 'sudo docker push phx.ocir.io/cloud_pursuit_appdev/sdhall/nginx:custom2'
            
           }
         }      
    }
}
