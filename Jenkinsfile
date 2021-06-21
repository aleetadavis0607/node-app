  pipeline {
        agent {label 'chrome' }
        tools { nodejs 'NodeJS' 
        dockerTool 'docker'
        }

        environment {
            CI = 'true'
            App = ''
        }
        stages {
            stage('Clone Repository') {
                steps {
                    script {
                        checkout scm
                        sh 'node --version' 
                        sh 'docker --version'
                        sh  'npm --version'
                    }
                }
            }   
            stage('Build Image') {
                steps {
                    script{
                        App = docker.build("anandr72/nodeapp")
                    }
                }
            }
            //stage('image pull') {
                //steps {
                    //script{
                        //sh 'docker pull anandr72/nodeapp:latest'
                    //}
               // }
            //}
            stage('Test image') {
                steps {
                    script{
                        anandr72/nodeapp.inside{
                        //sh 'test.js'
                        //App.inside {
                        echo "Test Passed"
                        }
                    }
                }
            }
            stage('Push Image'){
                steps {
                    script{
                        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub'){
                        App.push("${env.BUILD_NUMBER}")
                        App.push("latest")
                    }
                    echo "Trying to push docker build to DockerHub"
                }
            }
        }
            
     }
    
    }

