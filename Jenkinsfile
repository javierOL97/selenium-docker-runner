pipeline {

    agent any

    stages{

        stage('Run Test'){
            steps{
                bat "docker compose up"
            }
        }

        stage('Turn down Selenium Grid'){
            steps{
                bat "docker compose down"
            }
        }
    }
}