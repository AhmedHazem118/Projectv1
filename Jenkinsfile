pipeline {
    agent any

parameters{
choices (name: 'Version',choice: ['1.0','1.1'], description: 'Choose Version')
booleanParam (name: 'Exec', defaultValue: true, description: 'Build??' )
}
environment{
Version = '1.0'
}

    stages {
        stage("build") {
            steps {
            echo 'This Builds';
            }
        }
      stage("test"){
          steps {
when {
expression {
params.Exec
}
}
        echo 'This tests';
      }
      }
      stage("deploy"){
          steps {
echo "Deployed version is {$params.Version}"

      }
      }
    }
}
