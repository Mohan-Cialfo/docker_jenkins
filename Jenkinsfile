pipeline {
    agent { docker { image 'rust:1.31' } }
    stages {
        stage('build') {
            steps {
                sh 'rustc --version'
                sh ' docker build -t my-rust-lib .'
            }
        }
        stage('run test'){
            steps {
                sh 'docker run my-rust-lib cargo test'
            }
        }
        // stage('Deploy') {
        //     steps {
        //         retry(3) {
        //             sh './flakey-deploy.sh'
        //         }

        //         timeout(time: 3, unit: 'MINUTES') {
        //             sh './health-check.sh'
        //         }
        //     }
        // }
    }
    post {
        always {
            echo "build id ${BUILD_ID}"
            echo "build number ${BUILD_NUMBER}"
            echo "build tag ${BUILD_TAG}"
        }
        success {
            sh "docker tag my-rust-lib:latest mohanliucialfo/rust_sample:${BUILD_ID}"
            sh "docker push mohanliucialfo/rust_sample:${BUILD_ID}"
        }
    //     failure {
    //         echo 'This will run only if failed'
    //     }
    //     unstable {
    //         echo 'This will run only if the run was marked as unstable'
    //     }
    //     changed {
    //         echo 'This will run only if the state of the Pipeline has changed'
    //         echo 'For example, if the Pipeline was previously failing but is now successful'
    //     }
    }
}
