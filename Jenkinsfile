pipeline {
    agent {
        docker {
            image 'python:3.13.1'
            args '-u root:root'
        }
    }
    stages {
        stage('Parallel Testing') {
            parallel {
                stage('Python 3.13 Tests') {
                    steps {
                        sh 'python -m venv .venv_313'
                        sh '. .venv_313/bin/activate'
                        sh 'pip install -r requirements.txt'
                        sh 'pytest --html=report_313.html --self-contained-html'
                    }
                }
                
                stage('Python 3.12 Tests') {
                    steps {
                        sh 'python -m venv .venv_312'
                        sh '. .venv_312/bin/activate'
                        sh 'pip install -r requirements.txt'
                        sh 'pytest --html=report_312.html --self-contained-html'
                    }
                }
            }
        }
    }
}