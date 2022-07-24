pipeline {
    agent any

    stages {
        
         stage('Quality Scan') {
            steps {
               
            sh "mvn -Dmaven.test.failure.ignore=true clean compile"
               
            sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=algow-assignment \
  -Dsonar.host.url=http://54.226.50.200 \
  -Dsonar.login=sqp_432f7d193366457b1fad6a60c6ec1ebfc2c2f9a0"

               
            }

            
        }
        
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/saurabhd2106/maven-java-sample-app.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            
             post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
                success {
                    
                    archiveArtifacts 'target/*.jar'
                }
            }
            
        }
        
       
    }
}
