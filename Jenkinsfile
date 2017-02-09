node ("maven"){
   stage('Preparation') {
      git 'https://github.com/steven166/spring-boot-demo.git'
   }
   stage('Build Jar') {
     sh "chmod 777 ./gradlew"
     sh "./gradlew build"
   }
   stage('Build Docker') {
     sh "docker build -t maxxton2/demo-service:dev"
   }
   stage('Push Docker') {
     sh "docker push maxxton2/demo-service:dev"
   }
}