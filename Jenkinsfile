pipeline {
    agent any

    stages {
        stage('Clone Git Repository') {
            steps {
               git 'https://github.com/jorgegabrielti/jk-public-gh.git'
            }
        }
        stage('Building Image') {
            steps {
               sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }
        stage('Deploy Application') {
            steps {
               sh '''
                    docker stop webapp_ctr
                    sh docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
                  '''
            }
        }
        
    }
}
