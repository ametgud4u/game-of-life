

node('jfrognew'){
    stage('scm'){
	git 'https://github.com/ametgud4u/game-of-life.git'
    }

    stage('build'){
	sh label: '', script: 'mvn clean package'
   }
}
