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
               // build propagate: false,job: 'ListOldJobs', parameters: [string(name: 'Days', value: '2'), string(name: 'ID', value: '753704'), string(name: 'NODE', value: 'master')]
            }
        }

        stage('Copy artifacts'){
            steps{
                copyArtifacts filter: '*.txt', fingerprintArtifacts: true, projectName: 'ListOldJobs', selector: lastCompleted()
                //archiveArtifacts artifacts: '*.txt', followSymlinks: false
            }
        
        }
        stage('groovy'){
            steps{
                bat 'groovy getjobs.groovy'
            }
        }
    }
}

    

