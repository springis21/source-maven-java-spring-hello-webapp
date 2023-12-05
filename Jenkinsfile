pipeline {
  agent {
      label "jenkins-node"
  }

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout Stage') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/springis21/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Build Stage') {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
    stage('Test Stage') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy Stage') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://15.164.242.47:8080/')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}