pipeline {

    agent any

    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select a browser to execute the test suites.', name: 'BROWSER'
        choice choices: ['1', '2', '3', '4', '5'], description: 'Select the number of threads', name: 'THREAD_COUNT'
    }

    stages{

        stage('Start Selenium Grid'){
            steps{
                bat "docker compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
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