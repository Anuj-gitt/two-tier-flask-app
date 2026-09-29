pipeline {
    agent { label "dev" }

    stages {
        stage("Code") {
            steps {
                git url: "https://github.com/sarthujecrc/two-tier-flask-app.git",
                    branch: "main"
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t sarthu/flasksarthuapp ."
            }
        }

        stage("Test") {
            steps {
                echo "Testing application..."
            }
        }

        stage("Deploy") {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}
