node('master'){
    stage('scm'){
	git 'https://github.com/ametgud4u/game-of-life.git'
    }

    stage('build'){
	sh label: '', script: 'mvn clean package'
    }

    stage('Sonar') {
        withSonarQubeEnv('sonar') {
        sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
    }

    stage("Quality Gate") {
            steps {
              timeout(time: 30, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
    }
       stage('postbuild'){
       junit '**/pipeline-gameoflife/target/surefire/*.xml'
       archiveArtifacts 'target/*.jar'
   }
   }
  }
  }
}
