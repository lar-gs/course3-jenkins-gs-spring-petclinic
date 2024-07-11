pipeline {
    agent any {
        stage("build") {
            steps{
                sh "./mvnw package"    
            }
        }
        
        stage("capture") {
            steps {
                // "**/target/*.jar"
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'    
            }
        }
    }
    
    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                to:'always@foo.bar',
                recipientProviders: [developers()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [$env.BUILD_NUMBER}]"
                sleep 4
        }
    }
}
