node ("maven"){
   stage('Preparation') {
      git 'https://github.com/steven166/spring-boot-demo.git'
   }
   stage('Build Jar') {
     sh "chmod 777 ./gradlew"
     sh "./gradlew build"
     stash includes: 'Dockerfile', name: 'dockerfile'
     stash includes: 'build/libs/**', name: 'jar'
   }
}
node ("docker"){
   stage('Build Docker'){
     unstash name: 'dockerfile'
     unstash name: 'jar'
     sh 'docker build --no-cache -t maxxton2/demo-service:dev .'
   }
   stage('Push Docker'){
     sh 'docker push maxxton2/demo-service:dev'
   }
}