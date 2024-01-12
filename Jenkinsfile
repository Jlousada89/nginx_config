/* GITHUB_REPOSITORY: <your-repository-url>
GITHUB_BRANCH: main
JENKINS_JOB_NAME: deploy_nginx

on:
  push:
    branches:
      - $GITHUB_BRANCH

jobs:
  my-jenkins-job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Build
        run: echo "Building..."
*/

pipeline {
    agent any

    stages {
        stage('Clone Git Repository') {
                    git url: 'https://github.com/Jlousada89/nginx-config.git'
        }

        stage('Build Docker Image') {
            steps {
                docker build -t nginx:latest .
            }
        }

        stage('Deploy Docker Image') {
            steps {
                docker push nginx:latest
            }
        }

        stage('Copy Nginx Configuration File') {
            docker cp 'workspace/nginx.conf' 'my-nginx-container:/etc/nginx/nginx.conf'
        }

        stage('Update Nginx Configuration File') {
            docker exec my-nginx-container nginx -s reload
        }

        stage('Restart Nginx Service') {
            docker exec my-nginx-container nginx -s reload
        }
    }
}