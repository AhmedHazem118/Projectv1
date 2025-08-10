pipeline {
    agent any

    parameters {
        choice(name: 'Versions', choices: ['1.0', '1.1'], description: 'Choose Version')
        booleanParam(name: ' Exec', defaultValue: true, description: 'Do you want to test')
    }

    environment {
        VERSION = '1.0'  // Default value if not overridden by parameter
    }

    stages {
        stage("Build") {
            steps {
                echo 'This Builds'
            }
        }
        
        stage("Test") {
            when {
                expression { params.Exec }
            }
            steps {
                echo 'This tests'
            }
        }
        
        stage("Deploy") {
            steps {
                echo "Deployed version is ${params.Version}"
            }
        }
    }
}
