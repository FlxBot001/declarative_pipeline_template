pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'chmod a+x run_build_script.sh'
        sh './run_buld_script.sh'
      }
    }
    stage('Test') {
      parallel {
        stage ('Test on Windows') {
          steps {
            echo "Running tests on windows"
          }
        }
        stage ('Test on Linux') {
          steps {
            echo "Running tests on Linux"
          }
        }
      }
    }
    stage ('Confirm Deploy to staging') {
      steps {
        timeout (time: 60, unit: 'SECONDS') {
          input (message: 'Okay to Deploy?', ok: 'Let\'s Do it!')
        }
      }
    }
    stage ('Deploy to staging') {
      steps {
        echo "Deploying to staging..."
      }
    }
    stage ('Confirm Deploy to Production') {
      steps {
        timeout (time: 60, unit: 'SECONDS') {
          input (message: 'Okay to Deploy?', ok: 'Let\'s Do it!')
        }
      }
    }
    stage ('Deploy to roduction') {
      steps {
        echo "Deploying to production..."
      }
    }
  }
  post {
    success {
      echo "build succeeded"
    }
    failure {
      echo "Build failed"
    }
  }
}
