pipeline {
    agent {
        any{}
    }
    stages {
        stage('Build the docker image with tag') {
            steps {
            sh'''
              echo ${BUILD_NUMBER}
               git clone https://github.com/Balraj7887/helloworld-node.js.git;
               cd helloworld-node.js;
               docker build -t app:${BUILD_NUMBER} .;
               docker tag app:${BUILD_NUMBER} app:latest
              '''
            }
        }
       stage('Run the docker imaage') {
            steps {
               
               sh '''
               
               container_id=`docker ps | grep 0.0.0.0:80 | awk '{print $1}'`
               if [ ! -z "$container_id" ]; then
                docker stop $container_id
                docker rm $container_id
                fi
               
               docker run -d -p 80:3000 --restart always app:${BUILD_NUMBER}
               '''
               
            }
        }
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
