pipeline {
    agent any
    def app
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        
        stage('Buld Image'){
           app = docker.build('rajadockerimages/nodeapp')
        }
        stage('Tests')
        {            
            app.inside {
                echo "Tests passed"
            }
        }
        stage ('Push Image')
        {
            docker.withRegistry('https://registry.hub.docker.com','docker_hub_login' {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
            })
        }
    }
}
