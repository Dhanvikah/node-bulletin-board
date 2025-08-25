pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker-creds')
    GITHUB_CREDS = credentials('Git-Creds')
    IMAGE_NAME = "dhanvikah/node-bulletin-board"
    IMAGE_TAG = "${BUILD_NUMBER}-${GIT_COMMIT.take(7)}"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker image') {
      steps {
        script {
          sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -t ${IMAGE_NAME}:latest -f bulletin-board-app/Dockerfile bulletin-board-app"
        }
      }
    }

    stage('Push Docker image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Docker-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
          sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
          sh "docker push ${IMAGE_NAME}:latest"
        }
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

          script {
            def branch = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
            sh "git push origin HEAD:${branch}"
          }
        }
      }
    }

    stage('Trigger ArgoCD Sync') {
      steps {
        sh "argocd app sync node-bulletin-board || true"
      }
    }
  }
}
