node {
    stage('Clone Git Repository') {
        git 'https://github.com/<your-username>/<your-repository>.git'
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