node ("maven"){
   stage('Checkout') {
      // Checkout repository
      git 'https://github.com/steven166/spring-boot-demo.git'
   }
   stage('Build preparations'){
      // Create Build configuration
      sh 'oc process -f build-config.yml -v NAME=spring-boot-demo -v TAG=dev -v GIT_URL=https://github.com/steven166/spring-boot-demo.git | oc create -f -'
   }
   stage('Build') {
     // Start build and wait to finish it
     sh 'oc start-build spring-boot-demo --wait --folow'
   }
   stage('Build cleanup'){
     sh 'oc delete build/spring-boot-demo'
   }
}