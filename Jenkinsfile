pipeline {
agent any
environment {
DOCKER_HOME = tool name: 'MyDocker', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
}
stages {
stage('Example') {
steps {
sh 'docker -v'
sh 'echo $DOCKER_HOME'

}
}
}
}
