node('jfrognew'){
    stage('scm'){
	git 'https://github.com/ametgud4u/game-of-life.git'
    }

    stage('build'){
	   input 'continue to next step?'
	sh label: '', script: 'mvn clean package'
    }
    
     stage('postbuild'){
        junit '**/pipeline-gameoflife/target/surefire/*.xml'
        archiveArtifacts 'target/*.jar'
	    
    stage('SonarQube analysis') {
    // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
    withSonarQubeEnv('sonar') {
      // requires SonarQube Scanner for Maven 3.2+
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
    }
    }
  }
}
