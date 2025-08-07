pipeline {
    agent any
credit = credential('User')
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
echo "Add credentials ${credit}";


        echo "Deployed version ${Version}";
      }
      }
    }
}
