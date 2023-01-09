pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("krzysztofgurgacz/train-schedule2")
                    app.inside {
                        sh 'echo $(curl 18.207.248.189:8080)'
                    }
                }
            }
        }
    }   
}
