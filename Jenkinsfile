@Library('apwide-jenkins-shared-lib@develop')

def buildVersionName

pipeline {
    agent any
    environment {
      APW_JIRA_CLOUD_CREDENTIALS_ID = "jira-cloud-test-credentials"
      APW_GOLIVE_CLOUD_CREDENTIALS_ID = 'golive-cloud-test-credentials'
      APW_JIRA_CLOUD_BASE_URL = 'https://gigue.atlassian.net'
    }
    stages {
        stage('build') {
            steps {
                sh 'echo Build...'
            }
        }
        /*
        stage ('call jira api') {
            steps {
                apwCallJira httpMode: 'GET', path: '/rest/api/2/project'
            }
        }*/
        stage ('send deployment info to golive') {
            steps {
                script{
                    def pom = readMavenPom file: 'pom.xml' 
                    apwSendDeploymentInfo(application: 'eCommerce', category: 'PreProd', version: pom.version, buildNumber: currentBuild.number)
                }
            }
        }
        /*stage ('check golive environment statuses') {
            steps {
                apwCheckEnvironmentsStatus criteria:[categoryName: ['PreProd', 'Staging']]
            }
        }*/
        stage('success') {
            steps {
                sh 'echo Built'
            }
        }
    }
}
