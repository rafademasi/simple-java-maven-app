pipeline {
       agent any
       environment{
	JAVA_HOME="${tool 'Corretto'}"
       	PATH="${env.JAVA_HOME}/bin:${env.PATH}"
       }


stages {
        stage('Build') {
            steps {
                sh 'java -version'
		sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
