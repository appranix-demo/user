node {
   stage('Build') {
         git 'https://github.com/veereshwaran/user/'
         sh "echo build docker"
         sh "docker-compose build"
   }

   stage('Publish docker') {
       withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'veeresh-docker',
                            usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
          sh "echo push docker"
          sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
          sh "docker tag veeresh27/user:latest veeresh27/user:${env.BUILD_ID}"
          sh "docker push veeresh27/user:${env.BUILD_ID}"
          sh "docker rmi veeresh27/user:${env.BUILD_ID}"
          sh "docker rmi veeresh27/user:latest"
        }
   }

   stage('Deploy to CI') {
      sh "echo deploy to CI"
   }

   stage ("Approve To QA") {
          input message: "Proceed?"
    }

   stage('Deploy to QA') {
      sh "echo deploy to QA"
   }

   stage ("Approve To PROD") {
          input message: "Proceed?"
    }

   stage('Deploy to PROD') {
      sh "echo deploy to PROD"
   }
}
