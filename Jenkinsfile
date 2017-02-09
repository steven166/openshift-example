node {
   stage('Checkout') {
      // Checkout repository
      git 'https://github.com/steven166/spring-boot-demo.git'
   }
   stage('Build preparations'){
      try{
        // Delete old Build Config
        sh 'oc delete bc/spring-boot-demo'
      }catch(Exception e){}
      // Create Build Config

      sh 'oc process -f build-config.yml -v NAME=spring-boot-demo -v TAG=dev -v GIT_URL=https://github.com/steven166/spring-boot-demo.git | oc create -f -'
   }
   stage('Build') {
     // Start build and wait to finish it
     //sh 'oc start-build spring-boot-demo --wait --follow'
     openshiftBuild apiURL: '', authToken: '', bldCfg: 'spring-boot-demo', buildName: '', checkForTriggeredDeployments: 'true', commitID: '', namespace: '', showBuildLogs: 'true', verbose: 'false', waitTime: '', waitUnit: 'sec'

   }
}