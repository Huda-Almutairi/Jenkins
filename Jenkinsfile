pipeline {
    agent any
    options{
    skipDefaultCheckout()
    }
    
    stages {
        stage('checkout scm') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'GitHub-credentials', url: 'http://github.com/Huda-Almutairi/Jenkins.git'
                    sh 'git log --pretty=oneline --abbrev-commit | awk \'{print $1}\' ORS=\'\\n\' >>log.txt'
                }
            }
        }
        stage('get build Params User Input') {
            steps{
                script{
                    liste = readFile 'log.txt'
                    echo "please click on the link here to chose the branch to build"
                    env.COMMIT_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!',
                            parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
                }
            }
        } 
        stage("checkout the branch") {
            steps {
                echo "${env.BRANCH_SCOPE}"
                git branch: 'main', credentialsId: 'GitHub-credentials', url: 'http://github.com/Huda-Almutairi/Jenkins.git'
                sh "git checkout -b build ${env.BRANCH_NAME}"
            }
        }
        stage("exec maven build") {
            steps {
                withMaven(maven: 'M3', mavenSettingsConfig: 'mvn-setting-xml') {
                   sh "mvn clean install "
                }
            }
        }
        stage("clean workwpace") {
            steps {
                cleanWs()
            }
        }
    }
}
