pipeline {
        agent none
        stages {
		  stage("Checkout") {
            agent any
            steps {
                sh 'git clone https://github.com/gvsiva2008/Jenkins.git'
				sh 'cd Maven-simple'
            }
          }
          stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('My SonarQube Server') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        }
      }