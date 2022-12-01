node {
    
//     stage('Clone repo') {
//         git branch: "develop", url: "git@github.com:praveen1994dec/kubernetes_Jenkins_deployment.git", credentialsId: "githubcred"
//     }
    
    stage('SonarTests') {
        docker.image('newtmitch/sonar-scanner').inside('-v /var/run/docker.sock:/var/run/docker.sock --entrypoint=""') {
            sh "/usr/local/bin/sonar-scanner --version"
        }
    }
}
