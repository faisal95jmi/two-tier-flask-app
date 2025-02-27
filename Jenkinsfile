pipeline{
    agent any;
    stages{
        stage("Code Clone"){
            steps{
            git url: "https://github.com/faisal95jmi/two-tier-flask-app.git", branch: "master"
        }
    }
      stage("Build"){
            steps{
            sh "docker build -t two-tier ."
        }
    }
      stage("Test"){
            steps{
            echo "Test"
        }
    }
    
    stage("Push to Docker Hub"){
        steps{
    withCredentials([usernamePassword(credentialsId:"creds",
            passwordVariable: "dockerHubPass",
            usernameVariable: "dockerHubUser"
            )]){
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker image tag two-tier ${env.dockerHubUser}/two-tier "
            sh "docker push ${env.dockerHubUser}/two-tier:latest"
            
            }
    }
    }
      stage("Deploy"){
            steps{
           sh "docker compose up -d --build flask-app"
        }
    }
   
   
    }
}
