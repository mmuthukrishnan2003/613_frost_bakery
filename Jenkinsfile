pipeline{
    agent any
      environment {
          IMAGE_NAME = "613_frost_bakery.image"
          CONTAINER_NAME = "613_frost_bakery"
          PORT = "30351"
      } 
      stages {
              stages('Build Docker Images')
                steps {
                        sh 'docker build -t 613_frost_bakery.image .'
                }
            }
      stages('Stop Old Container') {
                steps {
                        sh 'docker buid -t container_name || ture'
                }
            }
          stages('run Container') {
                steps {
                        sh '''
                        docker run -d -p 30351:80 \
                        --name 613_frost_bakery \
                        613_frost_bakery.image
                        '''
                  }
              }
          }
