pipeline {
    agent any

    stages {
        stage('Fetch repository') {
            steps {
                git 'https://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@github.com/jlousada89/nginx_config.git'
            }
        }

        stage('Build and deploy container') {
            steps {
                sh 'docker build -t nginx:latest .'
                sh 'docker swarm init'
                sh 'TOKEN_COMMAND=$(docker swarm join-token worker)'
                sh 'TOKEN_COMMAND=$(echo ${TOKEN_COMMAND} | awk -F"command:" \'{print $2}\')'
                sh '${TOKEN_COMMAND}'
                sh 'docker service create -d --replicas 1 -p 80:80 nginx:latest'
            }
        }

        stage('Copy nginx.conf') {
            steps {
                sh 'scp nginx.conf <nginx-vm-user>@<nginx-vm-ip>:/etc/nginx/nginx.conf'
            }
        }

        stage('Restart httpd') {
            steps {
                sh 'ssh <nginx-vm-user>@<nginx-vm-ip> sudo systemctl restart nginx'
            }
        }
    }
}