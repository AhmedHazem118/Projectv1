pipeline {
    agent any

    parameters {
        choice(name: 'Versions', choices: ['1.0', '1.1'], description: 'Choose Version')
        booleanParam(name: 'Exec', defaultValue: true, description: 'Do you want to test')
    }

    environment {
        SCRIPT_FILE = "${params.Versions == '1.0' ? 'groovy.script' : 'groovy.scriptv1'}"
    }

    stages {
        stage("Build") {
            steps {
                script {
                    sc = load "${env.SCRIPT_FILE}"
                    sc.build()
                }
            }
        }
        
        stage("Test") {
            when {
                expression { params.Exec }
            }
            steps {
                script {
                    sc.test()
                }
            }
        }
        
        stage("Deploy") {
            steps {
                script {
                    sc.deploy()
                }
                echo "Deployed version is ${params.Versions}"
            }
        }
    }
}
