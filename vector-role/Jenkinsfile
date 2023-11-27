pipeline {
    agent any

    stages {
        stage('Clear work dir befor') {
            steps {
                deleteDir()
            }
        }
        stage('Sync Git') {
            steps {
                dir('vector-role') {
                    git branch: 'main', credentialsId: '9f1f1400-ed75-4579-bd4d-fb8849a0ceeb', url: 'git@github.com:danilabar/vector-role.git'
                }
            }
        }
        stage('Install molecule') {
            steps {
                sh "pip3 install 'molecule==3.4.0' 'molecule_docker'"
            }
        }
        stage('Check molecule') {
            steps {
                sh "molecule --version"
            }
        }
        stage('Start molecule test') {
            steps {
                dir('vector-role') {
                    ansiColor('xterm') {
                        sh "molecule test"
                    }
                }
            }
        }
        stage('Clear work dir after') {
            steps {
                deleteDir()
            }
        }
    }
}
