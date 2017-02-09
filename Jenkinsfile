node ("maven"){
   stage('Preparation') {
      git 'https://github.com/steven166/spring-boot-demo.git'
   }
   stage('Build Jar') {
     sh "chmod 777 ./gradlew"
     sh "./gradlew build"
     stash name: 'jar', includes: build/libs/demo.jar,Dockerfile
   }
}
node ("docker"){
   stage('Build Docker'){
     unstash name: 'jar'
     sh 'docker build --no-cache -t maxxton2/demo-service:dev .'
   }
   stage('Push Docker'){
     sh 'docker push maxxton2/demo-service:dev'
   }
}