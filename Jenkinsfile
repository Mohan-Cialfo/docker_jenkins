pipeline {
    agent { docker { image 'rust:1.31' } }
    stages {
        stage('build') {
            steps {
                sh 'rustc --version'
            }
        }
    }
}
