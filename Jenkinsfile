pipeline {
    agent any

    parameters {
        choice(name: 'Versions', choices: ['1.0', '1.1'], description: 'Choose Version')
        booleanParam(name: 'Exec', defaultValue: true, description: 'Do you want to test')  // Fixed space in parameter name
    }

    environment {
        VERSION = '1.0'  // Default value if not overridden by parameter
    }

    stages {
        stage("Build") {
            steps {
                script {
                    // Fixed: Proper Groovy syntax for method calls
                    sc = 'groovy.script' 
                    sc.build()  // Added parentheses for method call
                }
                echo 'This Builds'
            }
        }
        
        stage("Test") {
            when {
                expression { params.Exec }
            }
            steps {
                script {
                    sc.test()  // Added parentheses for method call
                }
                echo 'This tests'
            }
        }
        
        stage("Deploy") {
            steps {
                script {
                    sc.deploy()  // Added parentheses for method call
                }
                echo "Deployed version is ${params.Versions}"
            }
        }
    }
}
