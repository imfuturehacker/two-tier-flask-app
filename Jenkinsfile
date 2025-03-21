pipeline{
    
    agent any
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/imfuturehacker/two-tier-flask-app" , branch: "master"
                echo "Code cloned"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
                echo "code buld ho gyaaaaaa"
            }
        }
        stage("Test"){
            steps{
                echo "test phase"
            }
        }
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"DockerHubCreds",
                    passwordVariable: "DockerHubPass",
                    usernameVariable: "DockerHubUser")])
                    {
                        sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                        sh "docker image tag two-tier-flask-app ${env.DockerHubUser}/two-tier-flask-app"
                        sh "docker push ${env.DockerHubUser}/two-tier-flask-app:latest"
                    }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
                echo "deploy kar diyaaaa"
            }
        }
    }
}
