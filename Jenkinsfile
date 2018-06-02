pipeline {
    agent {
        label 'master'
    }
    environment {
        DOMAIN_NAME = 'haomingyin.com'
        PASSWORD = credentials('namecheap-ddns-password')
        SCRIPTS_REPO = 'https://github.com/haomingyin/namecheap-DDNS.git'
    }
    triggers {
        cron('H H * * *')
    }
    stages {
        stage('Pull Script') {
            steps {
                script {
                    sh "mkdir scripts"
                    sh "git clone ${env.SCRIPTS_REPO} ./scripts"
                }
            }
        }

        stage('Update DDNS Record - mac') {
            environment {
                HOST = 'mac'
            }
            steps {
                script {
                    dir('scripts') {
                        sh "./updateDNS.sh"
                    }
                }
            }
        }

        stage("Update DDNS Record - jenkins") {
            environment {
                HOST = 'jenkins'
            }
            steps {
                script {
                    dir('scripts') {
                        sh "./updateDNS.sh"
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }

}