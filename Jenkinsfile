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
                    if [[ $(docker stop webapp_ctr) ]]
                    then 
                      docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
                    else
                      docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}  
                    fi 
                  '''
            }
        }
        
    }
}
