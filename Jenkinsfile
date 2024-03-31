pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }   

         stage('Unit Test Artifact') {
            steps {
              sh "mvn test"
                   }


        }

         stage('Docker build stage') {
            steps {
             withDockerRegistry([credentialsId:"docker-hub",url:"https://docker.io/shanabdu"]){
              sh 'printenv'
              sh 'docker buildx build -t shanabdu/numeric-app:""$GIT_COMMIT"" .'
              sh 'docker push shanabdu/numeric-app:""$GIT_COMMIT""'
                   }
        }}

    }
}
