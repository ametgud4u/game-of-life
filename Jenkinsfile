

node('jfrognew'){
    stage('scm'){
	git 'https://github.com/ametgud4u/Devops.git'
    }

    stage('build'){
	sh label: '', script: 'mvn clean package'
    }

    stage('postbuild'){
	junit '**/target/surefire-reports/*.xml'
	archiveArtifacts 'target/*.jar'
    }
    
   stage('SonarScan') {
        withSonarQubeEnv('SONAR-7.1') {
             sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
    }

}
