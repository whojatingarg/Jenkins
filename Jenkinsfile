import jenkins.model.*
import hudson.model.*


pipeline{
    agent any 
    stages{
        stage('py version'){
            steps{
                bat 'python --version'
            }
        }
        stage('get jobs'){
            steps{
                build job: 'ListOldJobs', parameters: [string(name: 'Days', value: '2'), string(name: 'ID', value: '753704'), string(name: 'NODE', value: 'master')]
            }
            
        }
    }
}

    

