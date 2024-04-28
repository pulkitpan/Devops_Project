pipeline{
    agent any
    tools{
        maven 'MAVEN3'
    }
    
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/pulkitpan/registration-app.git'
            }
        }
        
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Archiving the Artifacts')
        {
            steps{
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false, onlyIfSuccessful: true
            }
        }
        stage('Reports')
        {
            steps{
                junit '**/*.xml'
            }
        } 
        stage('Approval')
        {
            steps{
                input 'Approve for Deployment'
            }
        }
 
        stage('Deploy to tomcat')
        {
            steps{
                 deploy adapters: [tomcat8(credentialsId: 'e018efd4-1a24-4e1d-9c92-997c771c930b', path: '', url: 'http://4.246.143.212:8080/')], 
                 contextPath: null, war: '**/*.war'
            }
        }
    }
}
