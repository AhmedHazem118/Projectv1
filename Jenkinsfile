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
        stage("Checkout Branch") {
            steps {
                script {
                    def branchName = ''
                    switch (params.Versions) {
                        case '1.0':
                            branchName = 'main'
                            break
                        case '1.1':
                            branchName = 'v1'
                            break
                        default:
                            error "Unknown version: ${params.Versions}"
                    }

                    echo "Checking out branch: ${branchName}"

                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${branchName}"]],
                        userRemoteConfigs: [[
                            url: 'https://github.com/your-org/your-repo.git'
                        ]]
                    ])
                }
            }
        }

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

