pipeline {
    agent any
    /* insert Declarative Pipeline here */
    stages {
        stage('run-test') {
            /* when {
                anyOf {
                    branch 'master'
                    branch 'dev'
                }
            } */
            steps {
                sh 'chmod +x ./gradlew'
                sh './gradlew test'
                jacoco(
                    classPattern: 'app/build/classes',
                    inclusionPattern: '**/*.class',
                    exclusionPattern: '**/*Test*.class',
                    execPattern: 'app/build/jacoco/**/*.exec'
                )
            }
        }
        stage('sonarqube-analysis') {
            environment {
                SONAR_TOKEN = credentials('sonarqube-token')
            }
            steps {
                sh '''./gradlew sonarqube \
 			-Dsonar.projectKey=D0649592-swimming-pool \
  			-Dsonar.host.url=http://140.134.26.54:10990 \
  			-Dsonar.login=6b859e7fe28b71f11c70a006c60b08c5057f3b54
                '''
            }
        }
    }
}
