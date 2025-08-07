pipeline {
    agent any
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
        echo 'This tests';
      }
      }
      stage("deploy"){
          steps {
        echo "Deployed version ${Version}";
      }
      }
    }
}
