def sc
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
            script {
                sc='groovy.script'
                sc.build
            }
            steps {
                echo 'This Builds'
            }
        }
        
        stage("Test") {
            script{
                sc.test
            }
            when {
                expression { params.Exec }
            }
        }
        
        stage("Deploy") {
            script {
                sc.deploy
            }
            }
        }
    }
}
