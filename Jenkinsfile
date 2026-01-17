pipeline {
  agent { label 'java_node' }
 
  stages {
    stage('Checkout') {
      steps {
        sh 'rm -rf *'
        sh 'git clone https://github.com/gsgeetha/bus_booking.git'
      }
    }
    stage('Build') {
      steps {
        withCredentials([usernamePassword(
            credentialsId: 'jfrog1',
            usernameVariable: 'JFROG_USER',
            passwordVariable: 'JFROG_API_KEY'
        )]){
        sh '''
          cd bus-booking
          git checkout feature-1
          mvn clean install
        '''
        }
      }
    }

    stage('Publish') {
      steps {
        sh '''
          cd bus-booking
          git checkout feature-1
          mvn clean deploy
        '''
      }
    }
    // stage('Run App') {
    //   steps {
    //     timeout(time: 1, unit: 'MINUTES') {
    //       sh 'java -jar */target/simple-parcel-service-app-1.0-SNAPSHOT.jar'
    //     }
    //   }
    // }
  }
}
