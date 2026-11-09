pipeline {
    agent none

    stages {
        stage('build') {
            agent {
                label 'buildnode'
            }
            steps {
                deleteDir()

                sh '''
                    git clone https://github.com/aslahaasla08-spec/deploy.git
                    ls -la
                '''

                stash name: 'webpage', includes: 'deploy/**'
            }
        }

        stage('deploy') {
            agent {
                label 'deploynode'
            }
            steps {
                deleteDir()

                unstash 'webpage'

                sh '''
                    rm -rf /var/www/html/*
                    cp -r deploy/* /var/www/html/
                    ls -la /var/www/html/
                '''
            }
        }
    }
}
