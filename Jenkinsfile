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
                sh "mkdir /var/lib/jenkins-test1"           
            }
        }
        stage("add a file"){
            steps{
                sh "touch /var/lib/jenkins-test1/file1.txt"
            }
            post{
                always{
                    archiveArtifacts artifacts: '/var/lib/jenkins-test1/file1.txt'
                }
            }
        }
    }
}
