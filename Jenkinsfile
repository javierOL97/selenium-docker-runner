pipeline {

    agent any

    stages{

        stage('Start Selenium Grid'){
            steps{
                bat "docker compose -f grid.yaml up -d"
            }
        }

        stage('Run Test Suites'){
            steps{
                bat "docker compose -f test-suites.yaml up"
            }
        }
    }

    post{
        always{
            bat "docker compose -f grid.yaml down"
            bat "docker compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'output/signup-test/emailable-report.html', followSymlinks:false
            archiveArtifacts artifacts: 'output/chill-suite/emailable-report.html', followSymlinks:false
            }
    }
}