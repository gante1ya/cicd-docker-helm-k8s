pipeline {

    agent any

    environment {
        registry = "gante1ya/vproappdock"
        registryCredential = 'dockerhub' 
    }

    stages {

        stage('BUILD') {
            steps {
                maven name: 'MyMaven', type: 'hudson.tasks.Maven', installation: 'MAVEN3'
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('UNIT TEST') {
            steps {
                sh 'mvn test'
            }
        }

        // ... Other stages ...

        stage('Build App Image') {
            steps {
                script {
                    dockerImage = docker.build "${registry}:V${BUILD_NUMBER}"
                }
            }
        }

        stage('Upload Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("V${BUILD_NUMBER}")
                        dockerImage.push('latest')
                    }
                }
            }
        }

        stage('Remove Unused docker image') {
            steps {
                sh "docker rmi ${registry}:V${BUILD_NUMBER}"
            }
        }

        stage('Kubernetes Deploy') {
            agent { label 'KOPS' }
            steps {
                sh "helm upgrade --install --force vprofile-stack helm/vprofilecharts --set appimage=${registry}:V${BUILD_NUMBER} --namespace prod"
            }
        }

    }

}
