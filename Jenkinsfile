node('master'){
    stage('scm'){
	git 'https://github.com/ametgud4u/game-of-life.git'
    }

    stage('build'){
	   input 'continue to next step?'
	sh label: '', script: 'mvn clean package'
	    
    stage("build & SonarQube analysis") {
          node {
              withSonarQubeEnv('My SonarQube Server') {
                 sh 'mvn clean package sonar:sonar'
              }
          }
      }

      stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }
   }
