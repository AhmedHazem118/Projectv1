
pipeline {
    agent any

    parameters {
        choice(name: 'Versions', choices: ['1.0', '1.1'], description: 'Choose Version')
        booleanParam(name: 'Exec', defaultValue: true, description: 'Do you want to test')  // Fixed space in parameter name
    }

    environment {
       SCRIPT_FILE = params.Versions == '1.0' ? 'groovy.script' : 'groovy.scriptv1'  // Default value if not overridden by parameter
    }

    stages {
        stage("Build") {
            steps {
                script {
                    // Fixed: Proper Groovy syntax for method calls
                  def sc = load "${env.SCRIPT_FILE}" 
                    sc.build()  // Added parentheses for method call
                }
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
