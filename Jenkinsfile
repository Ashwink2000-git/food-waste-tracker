pipeline {
    agent any 
    parameters {
        string(name: 'JIRA_ISSUE', defaultValue: 'DEV-123', description: 'Jira issue key for tracking')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Should tests be run?')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Ashwink2000-git/food-waste-tracker.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Food Waste Tracker...'
            }
        }
        stage('Test') {
            when {
                expression { params.RUN_TESTS } // Only run tests if the parameter is true
            }
            steps {
                echo 'Running tests...'
            }
        }
    }
    post {
        success {
            echo "Build succeeded with ID ${env.BUILD_ID}"
            jiraComment(issueKey: "${params.JIRA_ISSUE}", comment: "Build succeeded! Build ID: ${env.BUILD_ID}")
        }
        failure {
            echo "Build failed with ID ${env.BUILD_ID}"
            jiraComment(issueKey: "${params.JIRA_ISSUE}", comment: "Build failed! Build ID: ${env.BUILD_ID}")
        }
    }
}
