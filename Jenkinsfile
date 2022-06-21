// https://mvnrepository.com/artifact/org.jenkins-ci.main/jenkins-core

// @Grapes(
//      @Grab(group='org.jenkins-ci.main', module='jenkins-core', version='2.355')
// )

import org.jenkinsci.plugins.workflow.cps.CpsFlowDefinition

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
                bat 'python --version'
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
                
                     getJobs()
                
            }
        }
    }
}

    
@NonCPS
def getJobs(){

//def myParam = build.buildVariableResolver.resolve("Days")

def myParam = "${env.Days}"

println  "+-----------------------+ \n| No of days: " + myParam +"\t\t|\n+-----------------------+"

def cutOfDate = System.currentTimeMillis() - 1000L * 60 * 60 * 24 * 2

//def filename = build.workspace.toString() + "/jobs_lists.txt"
def filename =  "${WORKSPACE}" + "jobs_lists.txt"
targetFile = new File(filename).write("")
targetFile = new File(filename).append("<table><tr><th>Job Name</th><th>Last Build on</th><th>Keep</th><th>username</th></tr>")
println "Cut of Date: " + cutOfDate
for (job in Jenkins.instance.getAllItems(Job.class)) {
def build = job.getLastBuild()
if (build != null && build.getTimeInMillis() < cutOfDate) {
if (!job.getFullName().contains("MyAxis"))
if (!job.getFullName().contains("/"))
println job.getFullName() + " \033[31m Last build ona: \033[0m" + build.getTime().format("YYYY-MMM-dd HH:mm:ss") + "\n------------------------------------"
targetFile = new File(filename).append("<tr><td>"+job.getFullName() + "</td>" + "<td>"+ "Last build on: " + build.getTime().format("YYYY-MMM-dd HH:mm:ss") + "</td> <td></td><td></td></tr>"+ "\n")
}
}
targetFile = new File(filename).append("</table>")
    
}