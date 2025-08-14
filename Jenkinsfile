pipeline {
  options {
    ansiColor('xterm')
  }
  agent {
    docker {
      image 'node:22-alpine'
    }
  }

  environment {
    VITE_FF_DISABLE_BUGS = 'true'
  }

  stages {
    stage('build') {
      steps {
        sh 'npm ci'
        sh 'npm run build'
      }
    }

    stage('test') {
      steps {
        // Unit tests with Vitest
        sh 'npx vitest run --reporter=verbose'
      }
    }

    stage('deploy') {
      steps {
        // Mock deployment which does nothing
        echo 'Mock deployment was successful!'
      }
    }

    stage('e2e') {
        agent {
            docker {
                image 'mcr.microsoft.com/playwright:v1.54.2-jammy'
                reuseNode true
            }
        }

        environment {
            CI_ENVIRONMENT_URL_X = 'PUT YOUR NETLIFY SITE URL HERE'
        }

        steps {
            sh '''
                npx playwright test
            '''
        } 
    }   
  }
}


