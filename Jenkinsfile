// Scripted Pipeline
node {
    def dockerImage = 'node:16-buster-slim'
    def container

    try {
        container = docker.image(dockerImage).withRun('-p 3000:3000') {
            stage('Build') {
                sh 'apt-get update -y && apt-get install -y npm'
                sh 'npm install'
            }
            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
        }
    } finally {
        if (container != null) {
            container.stop()
        }
    }
}




// Declarative Pipeline
// pipeline {
//     agent {
//         docker {
//             image 'node:16-buster-slim'
//             args '-p 3000:3000'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//     }
// }