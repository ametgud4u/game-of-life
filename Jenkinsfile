node('$hostname'){
    stage('scm'){
	git 'https://github.com/ametgud4u/game-of-life.git'
    }
	
    stage('SonarQube analysis') {
    // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
    withSonarQubeEnv('sonar') {
      // requires SonarQube Scanner for Maven 3.2+
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
    }
    stage("Quality gate") {
           waitForQualityGate abortPipeline: true
            }
	    
    stage('build'){
	   input 'continue to next step?'
	sh label: '', script: 'mvn clean package'
    }
    stage('postbuild'){
        junit '/apps/workspace/GOL/gameoflife-build/target/surefire-reports/*.xml'
        archiveArtifacts 'target/*.jar'
    }
  }
}
