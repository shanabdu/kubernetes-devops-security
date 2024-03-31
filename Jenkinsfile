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
              sh 'printenv'
              sh 'docker buildx build shanabdu/numeric-app:""$GIT_COMMIT"" .'
              sh 'docker push shanabdu/numeric-app:""$GIT_COMMIT""'
                   }
        }

    }
}
