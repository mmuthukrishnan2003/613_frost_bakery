pipeline{
    agent any
      environment {
          IMAGE_NAME = "613_frost_bakery.image"
          CONTAINER_NAME = "613_frost_bakery"
          PORT = "30351"
      } 
      stages {
              stage('Build Docker Images'){
                steps {
                        sh "docker build -t ${IMAGE_NAME} ."
                }
            }
      stage('Stop Old Container') {
                steps {
                        sh "docker rm-f ${CONTAINER_NAME} || true"
                }
            }
          stage('Run Container') {
                steps {
                        sh """
                        docker run -d -p 30351:80 \
                        --name 613_frost_bakery \
                        613_frost_bakery.image
                        """
                  }
              }
          }
}
