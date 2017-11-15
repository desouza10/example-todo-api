node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
                sh 'php artisan config:cache'
            },
            'config route': {
                sh 'php artisan'
            }
        )
    }
    
    //Usuário do DockerHub
    stage('Docker Build') {
        sh 'docker build -t lgsouza12/todoapi:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push lgsouza12/todoapi:$BUILD_NUMBER'
    }
}
