pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url:"https://github.com/sarthujecrc/two-tier-flask-app.git",branch:"main"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t sarthu/flasksarthuapp ."
            }
        }
        stage("Test"){
            steps{
                echo "testing"
            }
        }
        stage("Docker Hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerhubrepo",
                    usernameVariable:"dockerhubuser",
                    passwordVariable:"dockerhubpassword"
                    )]){
                        sh 'docker login -u $dockerhubuser -p $dockerhubpassword'
                        sh 'docker image tag sarthu/flasksarthuapp $dockerhubuser/flask-app'
                        sh 'docker push $dockerhubuser/flask-app'
                    }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
