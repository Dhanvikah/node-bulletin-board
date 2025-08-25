pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker-creds')
    GITHUB_CREDS = credentials('Git-Creds')
    IMAGE_NAME = "komall6/node-bulletin-board"
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
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
          sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
          sh "docker push ${IMAGE_NAME}:latest"
        }
      }
    }

    stage('Update Helm values & push to Git') {
      steps {
        dir('helm') {
          withCredentials([usernamePassword(credentialsId: 'Git-Creds', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_TOKEN')]) {
            script {
              sh """
                # Update values.yaml tag
                sed -i 's/tag: .*/tag: "${IMAGE_TAG}"/' values.yaml || true

                # Configure Git
                git config user.email 'jenkins@ci.local'
                git config user.name 'jenkins'

                # Add and commit changes
                git add values.yaml
                git commit -m "ci: bump image tag to ${IMAGE_TAG}" || echo 'no changes to commit'

                # Get current branch
                branch=\$(git rev-parse --abbrev-ref HEAD)

                # Push using temporary basic auth
                git -c http.extraHeader="AUTHORIZATION: basic \$(echo -n ${GIT_USER}:${GIT_TOKEN} | base64)" push origin HEAD:\$branch
              """
            }
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
