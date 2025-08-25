pipeline {
  agent any
  environment {
    DOCKERHUB_CREDS = credentials('Docker-creds')  
    GITHUB_CREDS = credentials('Git-Creds')        
    DOCKER_REPO = "komall6/node-bulletin-board"
    IMAGE_TAG = "${env.BUILD_NUMBER}-${env.GIT_COMMIT?.substring(0,7)}"
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install & Test') {
      steps {
        dir('bulletin-board-app') {
          sh 'if [ -f package.json ]; then npm ci; fi'
          sh 'if [ -f package.json ] && grep -q "test" package.json; then npm test || true; fi'
        }
      }
    }

    stage('Build Docker image') {
      steps {
        sh "docker build -t ${DOCKER_REPO}:${IMAGE_TAG} -f bulletin-board-app/Dockerfile bulletin-board-app"
      }
    }

    stage('Login & Push Docker image') {
      steps {
        sh """
          echo ${DOCKERHUB_CREDS_PSW} | docker login -u ${DOCKERHUB_CREDS_USR} --password-stdin
          docker push ${DOCKER_REPO}:${IMAGE_TAG}
          docker logout
        """
      }
    }

    stage('Update Helm values & push to Git') {
      steps {
        dir('helm') {
          sh "sed -i 's/tag: .*/tag: \"${IMAGE_TAG}\"/' values.yaml || true"

          sh "git config user.email 'jenkins@ci.local' || true"
          sh "git config user.name 'jenkins' || true"

          sh "git remote set-url origin https://${GITHUB_CREDS_USR}:${GITHUB_CREDS_PSW}@github.com/${GITHUB_CREDS_USR}/node-bulletin-board.git"

          sh "git add values.yaml"
          sh "git commit -m 'ci: bump image tag to ${IMAGE_TAG}' || echo 'no changes to commit'"
          sh "git push origin HEAD:${env.BRANCH_NAME}"
        }
      }
    }
  }
  post {
    always { cleanWs() }
  }
}
