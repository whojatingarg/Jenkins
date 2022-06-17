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
                get_job()
            }
            
        }
    }
}


def get_job(){

    def cutOfDate = System.currentTimeMillis() - 1000L * 60 * 60 * 24 * 2

    def filename = Jenkins.build.workspace.toString() + "/jobs_lists.txt"
    targetFile = new File(filename).write("")
    targetFile = new File(filename).append("<table><tr><th>Job Name</th><th>Last Build on</th><th>Keep</th><th>username</th></tr>")
    println "Cut of Date: " + cutOfDate
    for (job in Jenkins.instance.getAllItems(Job.class)) {
    build = job.getLastBuild()
    if (build != null && build.getTimeInMillis() < cutOfDate) {
    if (!job.getFullName().contains("MyAxis"))
    if (!job.getFullName().contains("/"))
    println job.getFullName() + " \033[31m Last build ona: \033[0m" + build.getTime().format("YYYY-MMM-dd HH:mm:ss") + "\n------------------------------------"
    targetFile = new File(filename).append("<tr><td>"+job.getFullName() + "</td>" + "<td>"+ "Last build on: " + build.getTime().format("YYYY-MMM-dd HH:mm:ss") + "</td> <td></td><td></td></tr>"+ "\n")
    }
    }
    targetFile = new File(filename).append("</table>")

}
    

