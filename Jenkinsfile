
pipeline {
    agent any

    stages {
        stage('Display all commits') {
            steps {
                script {
                    sh '''
                        git log
                    '''
                }
            }
        }

    }
}
