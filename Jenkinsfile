pipeline{
    agent any
    options{
        timeout(time: 10, unit:'MINUTES')
    }
    stages{
        stage("make directory"){
            options{
                retry(2)
            }
            steps{
                sh "mkdir ~/jenkins-test"           
            }
        }
        stage("add a file"){
            steps{
                sh "touch ~/jenkins-test/file1.txt"
            }
            post{
                always{
                    archiveArtifacts artifacts: 'file1.txt'
                }
            }
        }
    }
}
