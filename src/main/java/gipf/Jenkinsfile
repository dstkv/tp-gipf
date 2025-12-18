pipeline {
    agent any
    
    stages {
        stage ("Clone le projet") {
            steps {
                git branch: 'master', url: 'https://github.com/dstkv/tp-gipf.git/'
            }
        }
        
        stage ("Compiler le projet") {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech.uphf.fr -D https.proxyPort=3128 compileJava"
            }
        }
        
        stage ("Vérifier le coverage avec JaCoCo") {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech.uphf.fr -D https.proxyPort=3128 test"
            }
        }
        
        stage ("Scanner avec Sonar") {
            steps {
                sh "./gradlew -Dhttps.proxyHost=proxy1-rech.uphf.fr -Dhttps.proxyPort=3128 sonar -Dsonar.projectKey=TPctrl -Dsonar.projectName='TPctrl' -Dsonar.host.url=http://172.17.0.1:9000 -Dsonar.token=sqp_7d73dd62bf8925925e13b459ebda39a2b253c7f4"
            }
        }
        
        stage ("Générer l'artifact .jar et l'archiver") {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech.uphf.fr -D https.proxyPort=3128 jar"
                archiveArtifacts artifacts: 'build/libs/*.jar'
            }
        }
    }
}
