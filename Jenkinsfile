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
            when {
                not {
                    branch 'PR-*'
                }
            }
            steps {
                script {
                    sh "mkdir scripts"
                    sh "git clone ${env.SCRIPTS_REPO} ./scripts"
                }
            }
        }

        stage('Update DDNS Record - mac') {
            when {
                not {
                    branch 'PR-*'
                }
            }
            environment {
                HOST = '*'
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
            when {
                not {
                    branch 'PR-*'
                }
            }
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