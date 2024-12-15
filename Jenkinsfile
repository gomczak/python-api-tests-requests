pipeline {
    agent none
    
    stages {
        stage('Parallel Testing') {
            parallel {
                stage('Python 3.13 Tests') {
                    agent {
                        docker {
                            image 'python:3.13.1'
                            args '-u root:root'
                        }
                    }
                    steps {
                        sh 'python -m venv .venv_313'
                        sh '. .venv_313/bin/activate'
                        sh 'pip install -r requirements.txt'
                        sh 'pytest --html=report_313.html --self-contained-html'
                    }
                    post {
                        always {
                            publishHTML([
                                allowMissing: false,
                                alwaysLinkToLastBuild: true,
                                keepAll: true,
                                reportDir: '.',
                                reportFiles: 'report_313.html',
                                reportName: 'Python 3.13 Test Report'
                            ])
                        }
                    }
                }
                
                stage('Python 3.12 Tests') {
                    agent {
                        docker {
                            image 'python:3.12.2'
                            args '-u root:root'
                        }
                    }
                    steps {
                        sh 'python -m venv .venv_312'
                        sh '. .venv_312/bin/activate'
                        sh 'pip install -r requirements.txt'
                        sh 'pytest --html=report_312.html --self-contained-html'
                    }
                    post {
                        always {
                            publishHTML([
                                allowMissing: false,
                                alwaysLinkToLastBuild: true,
                                keepAll: true,
                                reportDir: '.',
                                reportFiles: 'report_312.html',
                                reportName: 'Python 3.12 Test Report'
                            ])
                        }
                    }
                }
            }
        }
    }
}