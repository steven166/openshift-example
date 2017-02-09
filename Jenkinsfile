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
     docker.build("maxxton2/demo-service:dev")
   }
   stage('Push Docker'){
     docker.push("maxxton2/demo-service:dev")
   }
}